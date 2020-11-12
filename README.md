# Computer Vision API

Example Object Detection API using SSD_Resnet

#### Requirement
+ djangorestframework 
+ tensorflow
+ opencv
+ numpy
+ pillow

# Penggunaan Object Detection API

**Step 1, Download Model**

Download model SSD_Resnet pada link berikut https://bit.ly/3kjIPXv. lalu ekstrak ke direktori "simple_object_detection" dan ke direktori "my_api/app_object_detection"


**Step 2, Call API

Untuk pemanggilan API dapat menggunakan tools postman https://www.postman.com/, dengan spesifikasi request sebagai berikut

##### Method,

```
POST
```

##### End-Point,

```
http://127.0.0.1:8000/object_detection/api/
```

##### Request Header, 

```
Accept : application/json                    
Content-type : multipart/form-data
```                 

##### Request Param,

```
image : File, type=image/jpg
mode : integer, option= 1 or 2
```


# Tahapan Develop Object Detection API

**Step 1, Instalasi Library**

```
pip install djangorestframework
```

**Step 2, Create Django Project**

Buat projek baru menggunakan command berikut, dimana "my_api" pada tutorial ini merupakan nama projeknya.

```
django-admin startproject my_api
```

setelah command diatas dijalankan, akan terbentuk folder baru "my_api" dengan susunan direktori sebagai berikut,

    my_api
    │
    ├── my_api                    
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    │
    └── manage.py
    
**Step 3, Change Directory**

pindahkan direktori ke my_api

```
cd my_api
```
    
**Step 4, Create New Application**

Buat aplikasi baru menggunakan command berikut, dimana "app_object_detection" kita set sebagai nama aplikasinya.

```
python manage.py startapp app_object_detection
```

setelah command diatas dijalankan, akan terbentuk folder baru "app_object_detection". Dengan demikian direktori kita sekarang akan menjadi seperti berikut

    my_api
    │
    ├── my_api                    
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    │
    ├── app_object_detection                    
    │   ├── migrations
    │   │   └── __init__.py
    │   ├── __init__.py 
    │   ├── admin.py
    │   ├── apps.py
    │   ├── models.py
    │   ├── tests.py
    │   └── views.py
    │   
    └── manage.py
    
**Step 5, Define Method object_detection_api**

Source code Object Detection yang telah disusun sebelumnya, kita salin ke file "my_api/app_object_detection/views.py". Lalu kita edit menjadi seperti berikut

views.py ([view code](docs/archieve_views_v1.py))

**Step 6, Add csrf_exempt** 

Pastikan menambahkan tag @crsf_exempt diatas method object_detection_api, agar API dapat diakses tanpa menggunakan token

![alt text](docs/pic01.jpg)


**Step 7, Config End Point**

Import method object_detecion_api ke file "my_api/my_api/urls.py"

![alt text](docs/pic02.jpg)

lalu tambahkan end point yang diinginkan seperti contoh berikut ini,

![alt text](docs/pic03.jpg)

urls.py ([view code](docs/archieve_views_v1.py))

**Step 8, Add MEDIA URL**

Agar image hasil deteksi dapat diakses secara langsung dari client, perlu kita generate direct URL terhadap image yang tersimpan di server api. Untuk melakukan hal tersebut, tambahkan code berikut ke file "my_api/my_api/settings.py" di akhir line, seperti berikut ini,

```
import os
MEDIA_ROOT  = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

![alt text](docs/pic04.jpg)

import library berikut pada file "my_api/my_api/urls.py"

```
from django.conf.urls.static import static
from django.conf import settings
```

![alt text](docs/pic05.jpg)

tambahkan code berikut pada file "my_api/my_api/urls.py"

```
+ static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

![alt text](docs/pic06.jpg)

urls.py ([view code](docs/archieve_urls_v2.py))

**Step 9, Run API Server**

gunakan command berikut untuk menjalankan server API dalam mode development

```
python manage.py runserver
```


# Optimize Object Detection API

