# Media Files
> [source](https://timmyomahony.com/blog/static-vs-media-and-root-vs-path-in-django/)

in Main urls.py
```
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    # ... the rest of your URLconf goes here ...
]

if settings.DEBUG is True:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

