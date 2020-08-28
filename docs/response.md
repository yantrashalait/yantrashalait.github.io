# Response Format

Our standard response format for each API will be:

    {
        "ack": True or False,
        "msg": "Success or error message",
        "data": [] # if data is to be sent as a response
    }
Each response should include `ack` field. `msg` and `data` fields can be included
as per the response requirement. For example, a response of objection creation
API can only send `ack` and "Successfully created." as `msg`. Similarly, a detail
or list API will include `ack` and `data` fields in the response.

## How to write?
To send the response from your view:
  
    return Response({
        "ack": True,
        "msg": "Success"
    }, status=status.HTTP_200_OK)
    
    or,
    
    return Response({
        "ack": True,
        "data": serializer.data
    }, status=status.HTTP_200_OK)
    
Both `msg` and `data` can be included in the response if required. The status in 
`status.HTTP_200_OK` can be imported as:
    
    from rest_framework import status
