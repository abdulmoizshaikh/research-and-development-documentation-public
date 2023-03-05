# Apple-login-node

## Sheet 1

apple login rnd

1. get accesstoken in payload (JWT accesstoken)
2. decode jwt accesstoken get sub as user id and match this id with user id in request and then send response

Muhammad Usman, Jun 8, 12:14 PM

```bash showLineNumbers
curl -v POST "https://appleid.apple.com/auth/token" \
-H 'content-type: application/x-www-form-urlencoded' \
-d 'client_id=CLIENT_ID' \
-d 'client_secret=CLIENT_SECRET' \
-d 'code=CODE' \
-d 'grant_type=authorization_code' \
-d 'redirect_uri=REDIRECT_URI'
```

respnse of above call

After the server validates the authorization code, the endpoint returns the identity token, an access token, and a refresh token. The following is an example authorization validation response:

```json showLineNumbers
{
access_token: "adg61...67Or9",
token_type: "Bearer",
expires_in: 3600,
refresh_token: "rca7...lABoQ"
id_token: "eyJra...96sZg"
}
```

ref
https://developer.apple.com/documentation/sign_in_with_apple/generate_and_validate_tokens
https://developer.apple.com/documentation/sign_in_with_apple/tokenresponse

flutter: Calling API: https://dev-be.yallahood.com/api/users/login

flutter: Headers: {Content-Type: application/json; charset=UTF-8}

[log] Calling parameters: {providerId: 001755.85bbd82603d640269b0e4237b9b4076a.1532, provider: apple, authToken: ce02cef28533d41768cb0e9ac8807e50b.0.srxvv.Z4EFlk54SKnlChxljVluWA}

@Muhammad Moiz Shaikh https://pub.dev/packages/sign_in_with_apple. Server ki documentation check kr lo

Create a Sign in with Apple private key

To communicate with Sign in with Apple, you’ll use a private key to sign one or more developer tokens.

https://help.apple.com/developer-account/#/dev77c875b7e

Get a key identifier

https://help.apple.com/developer-account/#/dev646934554

## references

these are valid working references that I had impletemented

1. Generate and Validate Tokens https://developer.apple.com/documentation/sign_in_with_apple/generate_and_validate_tokens
2. TokenResponse https://developer.apple.com/documentation/sign_in_with_apple/tokenresponse

code

```jsx showLineNumbers
/**
_ @name socialValidator
_ @desc handle user login request
_ @params {string} accessToken
_ @params {string} provider
_ @returns {Promise}
_/
async function socialValidator(accessToken, provider) {
try {
let user = {};
if (provider === constants.ProviderType.GOOGLE) {
user = await fetchGoogleUser(accessToken);
} else if (provider === constants.ProviderType.FACEBOOK) {
user = await fetchFacebookUser(accessToken);
} else if (provider === constants.ProviderType.APPLE) {
user = await fetchAppleUser(accessToken);
}
return user;
} catch (err) {
throw err;
}
}
/**
_ @name fetchAppleUser
_ @desc fetch apple user details by userId and appToken
_ @params {string} accessToken
_ @returns {Object}
\*/
async function fetchAppleUser(accessToken) {
  try {
    // decode JWT access Token using JWT package
    const decode = jwt.decode(accessToken, { complete: true });
    // sub: userid,
    if (!decode) {
      throw new Error(AUTH_MESSAGES.INVALID_ACCESS_TOKEN_OR_PROVIDER_ID);
    }
    return {
      audience: decode?.payload?.aud,
      id: decode?.payload?.sub,
      email: decode?.payload?.email,
    };
  } catch (err) {
    throw err;
  }
}
```

## request object

register request

```json showLineNumbers
{
  "name": "Muhammad Usman",
  "email": "muhammad.usman@venturedive.com",
  "channelType": "app",
  "provider": "apple",
  "providerId": "001755.85bbd82603d640269b0e4237b9b4076a.1532",
  "authToken": "eyJraWQiOiJZdXlYb1kiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJodHRwczovL2FwcGxlaWQuYXBwbGUuY29tIiwiYXVkIjoiY29tLnlhbGxhaG9vZC55YWxsYWhvb2QiLCJleHAiOjE2MjQwMTAyMzksImlhdCI6MTYyMzkyMzgzOSwic3ViIjoiMDAxNzU1Ljg1YmJkODI2MDNkNjQwMjY5YjBlNDIzN2I5YjQwNzZhLjE1MzIiLCJjX2hhc2giOiJKV0NKYXRMeUMwcjJpS2lOdjY0X0ZBIiwiZW1haWwiOiJtdWhhbW1hZC51c21hbkB2ZW50dXJlZGl2ZS5jb20iLCJlbWFpbF92ZXJpZmllZCI6InRydWUiLCJhdXRoX3RpbWUiOjE2MjM5MjM4MzksIm5vbmNlX3N1cHBvcnRlZCI6dHJ1ZX0.bO8nmCIMmjSklRD-b5YAQzr-GxzruSvdNnq1UCD8ff8QV89n6gS6VfHoZ8AfVWdDvmOn2-ToOk3qSzD_AyGd0B_pGiZsZ0IwveTiALyk6mpX_zghGe7H9fRmr4onzOMkeRTgm6_GAQmXRsHAIG5QSBmV6vusOwMKI21-zx3yRQVqcdf8QJrY1iK3rl4oysecAWBoxWv1RIDmOa4hoMq2juTidC7Owy9Nl4L-h-TmPuLUgzPPJ-9EcuTNUOVp1qQWofhL5uUlxFWNj-dCvfBnxIekTLAK_C65odz4s9MJE6nF-MZPUoY-EYN_we-RD1lhI2kXqEmpUCzYvdkCtXsb6w"
}
```

**login request**

```json showLineNumbers
{
  "providerId": "001755.85bbd82603d640269b0e4237b9b4076a.1532",
  "provider": "apple",
  "authToken": "eyJraWQiOiJZdXlYb1kiLCJhbGciOiJSUzI1NiJ9.eyJpc3MiOiJodHRwczovL2FwcGxlaWQuYXBwbGUuY29tIiwiYXVkIjoiY29tLnlhbGxhaG9vZC55YWxsYWhvb2QiLCJleHAiOjE2MjQwMTAyMzksImlhdCI6MTYyMzkyMzgzOSwic3ViIjoiMDAxNzU1Ljg1YmJkODI2MDNkNjQwMjY5YjBlNDIzN2I5YjQwNzZhLjE1MzIiLCJjX2hhc2giOiJKV0NKYXRMeUMwcjJpS2lOdjY0X0ZBIiwiZW1haWwiOiJtdWhhbW1hZC51c21hbkB2ZW50dXJlZGl2ZS5jb20iLCJlbWFpbF92ZXJpZmllZCI6InRydWUiLCJhdXRoX3RpbWUiOjE2MjM5MjM4MzksIm5vbmNlX3N1cHBvcnRlZCI6dHJ1ZX0.bO8nmCIMmjSklRD-b5YAQzr-GxzruSvdNnq1UCD8ff8QV89n6gS6VfHoZ8AfVWdDvmOn2-ToOk3qSzD_AyGd0B_pGiZsZ0IwveTiALyk6mpX_zghGe7H9fRmr4onzOMkeRTgm6_GAQmXRsHAIG5QSBmV6vusOwMKI21-zx3yRQVqcdf8QJrY1iK3rl4oysecAWBoxWv1RIDmOa4hoMq2juTidC7Owy9Nl4L-h-TmPuLUgzPPJ-9EcuTNUOVp1qQWofhL5uUlxFWNj-dCvfBnxIekTLAK_C65odz4s9MJE6nF-MZPUoY-EYN_we-RD1lhI2kXqEmpUCzYvdkCtXsb6w"
}
```

## register controller code

**controller layer**

```jsx showLineNumbers
/**
 * @name registerUser
 * @desc register user and generate token
 * @params {Object} req
 * @params {Obejct} res
 * pass google id as string in request
 */
async function registerUser(req, res) {
  const { info, error } = logger("users/registerUser", "new");
  try {
    await AuthService.userValidation(req.body);
    info(init);
    req.body.email = req.body.email.toLowerCase();
    const { email, provider, providerId, authToken } = req.body;
    if (req.body.provider && req.body.authToken) {
      const dbUser = await AuthService.fetchUser({ provider_id: providerId });
      if (dbUser) {
        throw new Error(AUTH_MESSAGES.PROVIDER_ID_ALREADY_EXISTS);
      }
      const socialAuthRes = await AuthService.socialValidator(
        authToken,
        provider
      );
      // console.log('social validator socialAuthRes', socialAuthRes);

      if (req.body.providerId === socialAuthRes.id) {
        const { response, id } = await AuthService.createUser(req.body);
        info(`created: ${id}`);
        if (response) {
          res.json(response);
          info(responded);
          return;
        }
        res.json(response);
        info(responded);
      } else {
        throw new Error(AUTH_MESSAGES.INVALID_ACCESS_TOKEN_OR_PROVIDER_ID);
      }
    } else {
      const dbUser = await AuthService.fetchUser({ email });
      if (dbUser) {
        throw new Error(AUTH_MESSAGES.EMAIL_ALREADY_EXISTS);
      }
      const { response, id } = await AuthService.createUser(req.body);
      info(`created: ${id}`);
      if (response) {
        res.json(response);
        info(responded);
        return;
      }
      res.json(response);
      info(responded);
    }
  } catch (err) {
    console.log("err", err);
    error(err);
    const errRes = errorResponseNormalizer(err);
    res.status(statusCodes.BAD_REQUEST).json(errRes);
  }
}
```

## login-controller

**Controller code**

/\*\*

- @name userLogin
- @desc handler for user social login request
- @params {Object} req
- @params {Obejct} res
  \*/

```jsx showLineNumbers
async function userLogin(req, res) {
  const { info, error } = logger("users/userLogin", (req.body || {}).provider);
  try {
    await AuthService.userValidation(req.body);

    let response = {};
    if (req.body.email && req.body.password) {
      const { email, password } = req.body;
      info(init);
      response = await AuthService.userLogin({ email, password });
    } else {
      const { provider, providerId, authToken } = req.body;
      response = await AuthService.userLogin({
        provider,
        providerId,
        authToken,
      });
    }
    res.json(response);
    info(responded);
  } catch (err) {
    error(err);
    const errRes = errorResponseNormalizer(err);
    res.status(statusCodes.BAD_REQUEST).json(errRes);
  }
}
```

**service layer code**

/\*\*

- @name userLogin
- @desc handle user login request
- @params {string} accessToken
- @params {string} provider
- @returns {Promise}
  \*/

```jsx showLineNumbers
async function userLogin({ email, password, provider, providerId, authToken }) {
  try {
    let dbUser = {};
    if (email) {
      dbUser = await fetchUser({ email });
    } else {
      dbUser = await fetchUser({ provider_id: providerId });
    }
    if (!dbUser) {
      throw new Error(AUTH_MESSAGES.USER_NOT_FOUND);
    }
    // const socialAuthRes = await socialValidator(authToken, provider);
    const socialAuthRes = await socialValidator(
      authToken,
      provider,
      providerId
    );

    let user = {};
    if (provider && authToken) {
      if (providerId === socialAuthRes.id) {
        user = await userLoginHandler(dbUser);
      } else {
        throw new Error(AUTH_MESSAGES.INVALID_ACCESS_TOKEN_OR_PROVIDER_ID);
      }
    } else {
      user = await userLoginHandler(dbUser, password);
    }
    return user;
  } catch (err) {
    throw err;
  }
}
```
