# JWT Authentication in Django

## Authentication App

### JSON WebToken Authentication using `SimpleJWT`

## Libraries
`pip install djangorestframework-simplejwt`

 
### Changes
settings.py
```pycon
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    )
}
```

urls.py
```pycon
from django.urls import path
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)


urlpatterns = [
    path('token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('token/refresh/', TokenRefreshView.as_view(), name='token_refresh'),
]
```




## CORS Error

Resource: `https://github.com/adamchainz/django-cors-headers/tree/main`

`python -m pip install django-cors-headers`

```pycon
INSTALLED_APPS = [
    "corsheaders",
]

MIDDLEWARE = [
    ...,
    "corsheaders.middleware.CorsMiddleware",
    "django.middleware.common.CommonMiddleware",
    ...,
]
```
set one of - 
```pycon

    CORS_ALLOWED_ORIGINS
    CORS_ALLOWED_ORIGIN_REGEXES
    CORS_ALLOW_ALL_ORIGINS

```

```pycon
CORS_ALLOWED_ORIGINS = [
    'localhost'
]
```

## Adding Authenticaion on API

```py
from rest_framework.response import Response
from rest_framework.decorators import api_view
from rest_framework.decorators import permission_classes
from rest_framework.permissions import IsAuthenticated

@api_view(http_method_names=['GET'])
@permission_classes((IsAuthenticated,))
def my_data(request):
    return Response(dict(data='done'))

```