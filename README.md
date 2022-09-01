# JWTAuth
JWT authentication using ( Simple JWT package)
1-Install Packages
pip install djangorestframework
pip install djangorestframework-simplejwt
pip install django-filter


2-Add these apps in Installed app

INSTALLED_APPS = [
    '....',
    'rest_framework_simplejwt',
    'rest_framework',
]



3-Add this in settings.py 

REST_FRAMEWORK = {
    'DEFAULT_FILTER_BACKENDS': [
        'django_filters.rest_framework.DjangoFilterBackend'
    ],
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ],
}


4-Update URLs.py ( project Urls )

from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)

urlpatterns = [
    path('token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('token/refresh/', TokenRefreshView.as_view(), name='token_refresh'),
]

---------------------------------------------------------------------------------------------------------------------------
To Customize Token
1-Update URLs.py
urlpatterns = [
    # path('token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('token/', MyObtainTokenPairView.as_view(), name='token_obtain_pair'),
    path('token/refresh/', TokenRefreshView.as_view(), name='token_refresh'),
]

2-add revlevent view accordingly added in sample project (accounts.views)

--------------------------------------------------------------------------------------------------------------------------
default Settings 
DEFAULTS = {
    'ACCESS_TOKEN_LIFETIME': timedelta(minutes=5),
    'REFRESH_TOKEN_LIFETIME': timedelta(days=1),
    'ROTATE_REFRESH_TOKENS': False,
    'BLACKLIST_AFTER_ROTATION': True,

    'ALGORITHM': 'HS256',
    'SIGNING_KEY': settings.SECRET_KEY,
    'VERIFYING_KEY': None,
    'AUDIENCE': None,
    'ISSUER': None,

    'AUTH_HEADER_TYPES': ('Bearer',),
    'USER_ID_FIELD': 'id',
    'USER_ID_CLAIM': 'user_id',

    'AUTH_TOKEN_CLASSES': ('rest_framework_simplejwt.tokens.AccessToken',),
    'TOKEN_TYPE_CLAIM': 'token_type',

    'JTI_CLAIM': 'jti',

    'SLIDING_TOKEN_REFRESH_EXP_CLAIM': 'refresh_exp',
    'SLIDING_TOKEN_LIFETIME': timedelta(minutes=5),
    'SLIDING_TOKEN_REFRESH_LIFETIME': timedelta(days=1),
}

to update that settings simply override them in your settings.py 
Example (add this into settings.py )


from datetime import timedelta

SIMPLE_JWT = {
    'REFRESH_TOKEN_LIFETIME': timedelta(days=15),
    'ROTATE_REFRESH_TOKENS': True,
}

--------------------------------------------------------------------------------------------------------------------------
Reference
https://medium.com/django-rest/django-rest-framework-jwt-authentication-94bee36f2af8
https://django-rest-framework-simplejwt.readthedocs.io/en/latest/getting_started.html
