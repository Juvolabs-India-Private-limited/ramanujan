# Documentation on Network Pipeline
## Ramanujan

# Note
This documentation was last updated on 09:31 IST, 14 July 2020 by @t0xic0der.

# Introduction
The network pipeline for the project is an REST API built on the Django web framework. Being stateless in nature, either Django REST framework or FastAPI could have been a better choice but writing the API ground up using simply Django helps in facilitating the scalability of the application. The API makes use of HTTP requests for the transaction of JSON objects to and from the server. It has been written in a way in which it can be language-agnostic, hence wrapping the API around any kind of application - be it an mobile application, desktop software or a website, should be a piece of cake.

# Construction
As the actual implementation of Ramanujan involves getting the image file from the user, reading it for any textual content of any mathematical expression, solving the obtained mathematical expression and then finally returning the solution to the user - the API is made low-level to actually follow the stages exhibited by the underlying driver code. Hence there are three underlying applications in the API.

1. **`user2read`** - This application receives an image file from the user and sends it over to the expression recognition and detection system. The output of this application is a mathematical expression in string format.
2. **`read2solv`** - The output of `user2read` application is then conveyed as an input to this application where the mathematical expression string is evaluated with Python's standard `eval` procedure. The obtained result is in string format.
3. **`solv2user`** - The output of `read2solv` application is then conveyed as an input to this application where the evaluated result is sent back to the `conduit` application. This is then sent back to user as the final output.
4. **`conduit`** - This is a proto-application which acts as a layer of contact between the user and the other three applications. This sends the file to the `user2read` application and receives the output from the `solv2user` application.

# Details

1. **Why did you prefer to use multiple applications when you could have done it all in a single application?**  
The use of multiple small applications keeps the code granular and low-level, hence ensuring that every part of the API corresponds properly to their respective driver code. The granularity further helps in development and fixing of a specific application, should it require maintenance while keeping the other parts of the API safe and untouched.

2. **What is the performance hit that the API takes when conversing amongst the applications?**  
There is a marginal performance degradation which might lead to slow donws as less as ~1e-6 seconds due to the fact that the transaction among the multiple applications occur via requests and not by variable sharing.

3. **Why did you use a proto-application called `conduit` when you could have done with just three applications?**  
In the hindsight, the purpose of the `conduit` application is as meagre as receiving files from the user and sending the result back to the user. If you look closely, this lets you keep your other core applications safe by being easily switchable during any kind of availability attacks.

