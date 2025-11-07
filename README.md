- 👋 Hi, I’m @DuardusDuarnido
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
DuardusDuarnido/DuardusDuarnido is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
> ## Description
> 
> Requests sent to `https://api.getgems.io` through CloudFront **fail when the `User-Agent` header is empty or missing**. CloudFront responds with a **403 Forbidden** error.
> 
> Some clients and crawlers legitimately send requests with no `User-Agent`. These requests should either be proxied to the origin or rejected with a more meaningful error — but not blocked with a generic 403.
> 
> ---
> 
> ## Steps to Reproduce
> 
> 1. Send a request to the API without a `User-Agent` header, or with it explicitly set to empty. For example:
> 
>    ```bash
>    curl -H "User-Agent:" https://api.getgems.io/path/to/resource
>    ```
> 2. Check the response.
> 
> ---
> 
> ## Actual Result
> 
> * Response: **403 Forbidden**.
> 
> ---
> 
> ## Expected Result
> 
> * CloudFront should:
> 
>   * Forward the request to the origin unmodified, **OR**
>   * Return a clear error message instead of a generic 403.
> 
> ---
> 
> ## Impact
> 
> * Breaks scripts, bots, and monitoring tools that don’t set a `User-Agent`. (Such as .NET's Default HttpClient)
> * Leads to inconsistent behavior compared to standard HTTP servers (which usually accept empty/missing `User-Agent` values).
> 
> ---
> 
> ## Possible Causes
> 
> * CloudFront may enforce a built-in security rule that blocks empty or missing `User-Agent` headers by default.
> * Could be tied to AWS WAF or bot protection rules.
> 
> ---
> 
> ## Suggested Fix
> 
> * Allow requests with empty/missing `User-Agent` headers to pass through normally, **or** add a important notice to api docs
> 

