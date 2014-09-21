BungieNetPlatform
=================


Original Forum link
https://www.bungie.net/en/Forum/Post/68778685/0/0


Since there are some people here, I'll give a quick overview of how it currently works.

  Responses from bungie.net are JSON encoded, so that's why JSON.NET is included

 Currently, class constructors take JObjects which are those parsed by JSON.NET from the response from bungie.net. Those constructors then do the conversion into C# and .NET types. Example. The current code to do a lot of this is woefully incomplete though.

 The classes do try to mimic the serialised objects from bungie.net as closely as possible (which I think it probably what we should aim for at the very least), but do and probably should also include any additional functionality that can be provided. Example.

 Making requests to the Platform requires you pass a RequestingUser object to each exposed service method in the Platform class. The reason for this is to manage any cookie values and other little bits of information you might need to send, although it's admittedly not the best design. This is also the mechanism I'm using to make authorised requests using an authenticated Google account, although you won't find that code in there ;)

 Since the Platform class is essentially a series of IO bound methods, they should all return a Task<T> from an async method. That's my view anyway. but obviously they shouldn't if for whatever reason it needs to be synchronous..

 The IPlatform interface Platform implements probably doesn't need to exist. I was just using it for WCF stuff with pipes.

//

What I would like to do is divide and conquer; split up implementing the classes into separate groups: forums, users, destiny, etc... and anyone willing to write up the code for a particular group or sub group can take it on board (assigned via GitHub to keep track of things though).
