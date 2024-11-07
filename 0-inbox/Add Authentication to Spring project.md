- [ ] Authorization 
	- [ ] Use a JWT token. Need to filter like in server api security classes. 
	- [ ] Make a controller for both ways to authenticate: API key and username/password
		- [ ] filter might be used for both? 
	- [ ] If authenticated, user can access endpoints
Notes about authorization: 
SwaggerConfig tells swagger that bearer auth should be used. 
Each endpoint should have the annotation: security = {  
            @SecurityRequirement(name = "bearerAuth")  
        }
Need to add Spring Security as a dependency in POM
Look up a tutorial on Spring Security Config - the server api SecurityConfig is a good starting place, but different
Need: a dependency for spring security, a configuration, and a class which does the jwt validation
JWT will extract info. Look at the class `JWTTokenValidator` and the secret key in `maptripapi.properties`. The `JWTFilter` uses the servlet filter to say that before each request, this needs to happen. The `SecurityConfig` created the filter chain which tells what needs to happen. An important line is `http.sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS);`

11/06 Ending in SecurityConfig which needs a CustomAuthenticationEntryPoint (or does it?)