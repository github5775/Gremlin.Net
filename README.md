# Gremlin.Net
This is an adapted version of the [Gremlin.Net](https://github.com/apache/tinkerpop/tree/master/gremlin-dotnet) project that is part of [apache/tinkerpop](https://github.com/apache/tinkerpop).  I wanted to limit this repository to only the .Net library, because the parent is quite large and unwieldy if the user is only interested in .Net.  This is a modification of the earlier modification that I made for tinkerpop at large, making its use abstracted away from the calling code, which no longer must have any knowledge of server connection issues.

I have modified it to handle the case where the server has dropped the connection without notifying the client.  In that case, the call to the server will hang until it times out, sometimes up to 60 seconds!  Essentially, this modification forces the client to check the connection status before submitting the request.  In the case where the status of the connection is not open, the modification will refresh the connection, then send the request.  This allows the code that calls this layer to not require any knowledge of this process.

Conceptually, if the server drops the connection, the client should update itself.  In practice, however, this hack has been working great for me with no errors for about six months on a well-used production app whose data is ALL Cosmos Db Graph API.'

## Update - Parent Project Appears to be fixed
Please take a look at Apach Tinkerpop, as I have tested updated code, and it appears to handle connection timeouts more efficiently now.
