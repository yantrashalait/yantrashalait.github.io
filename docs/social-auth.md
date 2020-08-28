# Social authentication API

We will use `social-auth-app-django` for integrating social authentication in our
systems. The official documentation can be found in http://python-social-auth.readthedocs.org/

## Setup

    pip install social-auth-app-django
Add `social_django` to your INSTALLED_APPS. Then migrate:

    python manage.py migrate

Now we need to choose which social backends we shall use in our system. We can specify
that in the AUTHENTICATION_BACKENDS as:

    AUTHENTICATION_BACKENDS += [
        'social_core.backends.google.GoogleOAuth2',
        'social_core.backends.facebook.FacebookOAuth2',
    ]
GoogleOAuth2 is for google login, FacebookOAuth2 is for facebook login and so on.
You can find information about other backends from the official documentation.

Now in our __local_settings.py__ file, we will include the keys to be used for social
authentication to work. There are different keys required for each authentication
backend, for example, google login will have it's own set of keys different from
keys required for facebook.

## Key Setup

You can find the key information to be filled for each authentication backend from
the official documentation. I will only discuss about Google and Facebook authentication
in this documentation.

### For Google

    SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = "google_auth_key/public_key"
    SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = "google_auth_secret_key"
    SOCIAL_AUTH_URL_NAMESPACE = 'social'
    
    SOCIAL_AUTH_GOOGLE_OAUTH2_IGNORE_DEFAULT_SCOPE = True
    SOCIAL_AUTH_GOOGLE_OAUTH2_SCOPE = [
        'https://www.googleapis.com/auth/userinfo.email',
        'https://www.googleapis.com/auth/userinfo.profile',
    ]
We can find such keys in the developer console of Google. Also, you can search
in your browser for how to generate such keys.

### For Facebook

    SOCIAL_AUTH_FACEBOOK_KEY = "facebook_public_key"
    SOCIAL_AUTH_FACEBOOK_SECRET = "facebook_secret_key"
    
    SOCIAL_AUTH_FACEBOOK_SCOPE = ['email']
You can find the keys required above from facebook developers console.

## Pipeline
Pipelines are essential components for social authentication in Django. They 
help us to perform various operations before and after social authentication.
Along with this, they help us to define what operations are to be included and
what are to be excluded for social authentication.

Pipeline is useful for us to determine whether we need to use the social authentication
for login only or both login and registration. For our system, we will use both
login and registration. So, we need to make sure that `social_django` knows what
operations are to be done and what is the flow for authentication. We specify this
inside the pipeline in our __local_settings.py__ or __settings.py__ file:

    SOCIAL_AUTH_PIPELINE = (
        'social_core.pipeline.social_auth.social_details',
        'social_core.pipeline.social_auth.social_uid',
        'social_core.pipeline.social_auth.auth_allowed',
        'social_core.pipeline.social_auth.social_user',
        'social_core.pipeline.user.get_username',
        'social_core.pipeline.social_auth.associate_by_email',
        'social_core.pipeline.user.create_user',
        'social_core.pipeline.social_auth.associate_user',
        'social_core.pipeline.social_auth.load_extra_data',
        'social_core.pipeline.user.user_details',
    )
This pipeline is used for both user login and user creation. The manually registered
user can also be able to login using __"Login with Google"__ button as the users are
associated with email(specified in pipeline).

## How Does it Work?
After using `social_django` in our `INSTALLED_APPS` and migrating, few tables are 
created in our database, for instance, SocialAuthUser. This table holds the information
of the users that are associated with "Google Login" or "Facebook Login". This table
holds the information of our django user using a foreign key to the user table.

Now whenever an un-registered user tries to login to the system using social login,
entry for the user is created in both the social auth table and django user table.

Similarly, if a manually registered user tries to login with social auth, a new record
is created in the social auth table and user is logged in by associating his/her
email which he/she had entered during manual registration.

Social Login and Registration can be obtained from same API.

## Jumping into API Creation

After the setup is done, we can create API for social authentication. For this, 
in our `auth.py` file inside api.urls folder, we need to create a urlpattern as:

    from django.conf.urls import url
    
    auth_url_patterns = [
        '...'
        url(r'^exchange-token/(?<backend>[^/]+)$', view_name)
    ]
The `backend` specified in the url is the named of the backend(google or facebook).
This API will be hit from the front-end or mobile application in such manner:

    http://localhost:8000/api/v1/exchange-token/google-oauth2 # for google
    http://localhost:8000/api/v1/exchange-token/facebook # for facebook
Now we need to create a view for social authentication API.

So let's move towards the viewsets folder of api app and inside the `auth.py` file
of viewsets, we create a api_view as:
    
    import json
    
    from django.contrib.auth import get_user_model
    from django.views.decorators.csrf import csrf_exempt
        
    from social_django.utils import psa, load_strategy, load_backend
    
    User = get_user_model()
    
    @csrf_token
    @psa('social:complete')
    def exchange_token(request, *args, **kwargs):
        # return error message if request method is not POST
        if request.method != "POST":
            return Response({
                "ack": False,
                "msg": "Method not allowed"
            })
        else:
            # get access_token from the request data
            request_body = json.loads(request.body)
            access_token = request_body.get("access_token", "")
            
            # check if access_token is None or empty
            if not access_token or access_token == "":
                return Respose({
                    "ack": False,
                    "msg": "Access Token is missing."
                })
            try:
                ## this is the part where actual authentication is performed.
                ## user_req is the actual user for our system.
                user_req = request.backend.do_auth(access_token)
            except Exception as e:
                return Response({
                    "ack": False,
                    "msg": "Authentication failed."
                })
            if user_req and user_req.is_active:
                ## ToDo: generate the user token for the authenticated user.
                ## send the token as a Response

So, let's go through the code to understand it. 

First we have declared a function `exchange_token` where we have used two decorators,
csrf_token and psa. `csrf_token` is used to prevent any CSRFToken error that may
arise when request is made from the front-end or mobile application to this endpoint.

Similarly, `psa` is used to define the type of authentication this view performs.
'social:complete' helps the view to perform the final completion of authentication.

This view will require an `access_token` to authenticate the user. This `access_token`
is obtained from the front-end application. The request data shoould be sent in
raw JSON format. 

Now, if the request method is a POST method and access_token is also sent in the
request, our view proceeds to authenticating the user. `request.backend.do_auth` is 
responsible for authenticating the user. `request.backend` will change as per
the `backend` specified in the url. The `do_auth` function for each authentication
backend is different to each other.

If the user is authenticated successfully, a token is generated for the user and 
is sent out as a Response.
