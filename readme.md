# AIGC DAO Framework, the Gen-img Module
![MIT License](https://img.shields.io/badge/License-MIT-green.svg)

## Introduction
AI-Generated Content (AIGC) refers to digital creations produced by artificial intelligence, such as text, images, music, and videos. Tools like Llama, GPT for text, and Midjourney, DALL·E for images are making content creation faster and more accessible.

This open-source framework consists of several key modules that work together to provide a complete solution for AIGC generation and verification. 

The Content Generation and Inference module is responsible for generating actual content from AI models, such as text, images, audio, etc. (The framework will initially focus on the image generation domain.) Through AIGC DAO’s open-source framework, creators can call upon various AI models to generate content that meets their needs. These generated contents will be processed through model inference and output the works that best meet the requirements.

This is a management backend for Stable Diffusion image generation, part of the Content Generation and Inference module. It provides APIs to support text-to-image, image-to-image, ControlNet, image upscaling, and more. It also supports uploads to cloud storage services such as AWS and Qiniu. The platform utilizes asynchronous workers and supports multiple instances of Stable Diffusion, allowing for distributed processing.

---

## Table of Contents
1. [Deployment](#deployment)
2. [REST Framework Web Error](#rest-framework-web-error)
3. [Issues](#issues)
   - [Demjson 2.2.4 Error](#demjson-224-error)
   - [Collect Static Files](#collect-static-files)
   - [MySQL Client Installation](#mysql-client-installation)
4. [Initialize](#initialize)
5. [Create Superuser](#create-superuser)
6. [Project Manager](#project-manager)

---

## Deployment
Deploy the project to `/home/work`.

## REST Framework Web Error
If you encounter the following CSRF error in your REST framework:
```python
ajax: {"detail":"CSRF Failed: CSRF token missing or incorrect."}

setting.py:
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework.authentication.TokenAuthentication',
    )
}

```


# 2 Q&A
## Demjson 2.2.4 Error
To resolve the demjson 2.2.4 error, upgrade setuptools:

```bash
pip install --upgrade setuptools==57.5.0
```

## Collect Static Files
Run the following command to collect static files:
```bash
python manage.py collectstatic
```
Ensure your database is created with the correct character set:

```bash
CREATE DATABASE ai_draw_plat_v1 CHARACTER SET utf8mb4;
```

## MySQL Client Installation
Install the MySQL client based on your operating system:
```bash
pacman -S python-mysqlclient

CentOS

yum install mysql-devel -y
yum install python-devel -y
pip install mysqlclient -y

Ubuntu

apt-get install libmysql-dev
apt-get install libmysqlclient-dev
apt-get install python-dev #python3要装python3-dev
pip install mysqlclient

```

# Initialize
Run the following commands to initialize your database:


```bash
(venv) root@VM-8-5-ubuntu:/home/work/ai_draw_plat_v1# python manage.py makemigrations --settings=ai_draw_plat_v1.settings_prod api_auth
/home/work/ai_draw_plat_v1/logs
env: prod
{'114.240.225.0|7861': <lib.sdwebuiapi.webuiapi.webuiapi.WebUIApi object at 0x7f8062b0c340>}
Utils... /home/work/ai_draw_plat_v1/medias
[<URLPattern '^medias/(?P<path>.*)$'>]
System check identified some issues:

WARNINGS:
?: (urls.W005) URL namespace 'stabel_diffusion' isn't unique. You may not be able to reverse all URLs in this namespace
Migrations for 'api_auth':
  apps/api_auth/prod_migrations/0001_initial.py
    - Create model ApiUser
(venv) root@VM-8-5-ubuntu:/home/work/ai_draw_plat_v1# python manage.py makemigrations --settings=ai_draw_plat_v1.settings_prod stable_diffusion
/home/work/ai_draw_plat_v1/logs
env: prod
{'114.240.225.0|7861': <lib.sdwebuiapi.webuiapi.webuiapi.WebUIApi object at 0x7fb8b203c340>}
Utils... /home/work/ai_draw_plat_v1/medias
[<URLPattern '^medias/(?P<path>.*)$'>]
System check identified some issues:

WARNINGS:
?: (urls.W005) URL namespace 'stabel_diffusion' isn't unique. You may not be able to reverse all URLs in this namespace
Migrations for 'stable_diffusion':
  apps/stable_diffusion/prod_migrations/0001_initial.py
    - Create model TaskParams
    - Create model AsyncTask
(venv) root@VM-8-5-ubuntu:/home/work/ai_draw_plat_v1# python manage.py makemigrations --settings=ai_draw_plat_v1.settings_prod 
/home/work/ai_draw_plat_v1/logs
env: prod
{'114.240.225.0|7861': <lib.sdwebuiapi.webuiapi.webuiapi.WebUIApi object at 0x7fd3c67cf1f0>}
Utils... /home/work/ai_draw_plat_v1/medias
[<URLPattern '^medias/(?P<path>.*)$'>]
System check identified some issues:

WARNINGS:
?: (urls.W005) URL namespace 'stabel_diffusion' isn't unique. You may not be able to reverse all URLs in this namespace
Migrations for 'django_celery_results':
  venv/lib/python3.10/site-packages/django_celery_results/migrations/0009_auto_20230723_1645.py
    - Alter field id on chordcounter
    - Alter field id on taskresult
(venv) root@VM-8-5-ubuntu:/home/work/ai_draw_plat_v1# python manage.py migrate --settings=ai_draw_plat_v1.settings_prod 
/home/work/ai_draw_plat_v1/logs
env: prod
{'114.240.225.0|7861': <lib.sdwebuiapi.webuiapi.webuiapi.WebUIApi object at 0x7feb916e31f0>}
Utils... /home/work/ai_draw_plat_v1/medias
[<URLPattern '^medias/(?P<path>.*)$'>]
System check identified some issues:

WARNINGS:
?: (urls.W005) URL namespace 'stabel_diffusion' isn't unique. You may not be able to reverse all URLs in this namespace
Operations to perform:
  Apply all migrations: admin, api_auth, auth, contenttypes, django_celery_results, sessions, stable_diffusion
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0001_initial... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying api_auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying django_celery_results.0001_initial... OK
  Applying django_celery_results.0002_add_task_name_args_kwargs... OK
  Applying django_celery_results.0003_auto_20181106_1101... OK
  Applying django_celery_results.0004_auto_20190516_0412... OK
  Applying django_celery_results.0005_taskresult_worker... OK
  Applying django_celery_results.0006_taskresult_date_created... OK
  Applying django_celery_results.0007_remove_taskresult_hidden... OK
  Applying django_celery_results.0008_chordcounter... OK
  Applying django_celery_results.0009_auto_20230723_1645... OK
  Applying sessions.0001_initial... OK
  Applying stable_diffusion.0001_initial... OK
```

# Create Superuser

To create a superuser, run the following commands:


> login super user. create auth user and openid and setting position:  ai_draw_plat_v1/views.py:64

```bash
python manage.py makemigrations --settings=ai_draw_plat_v1.settings_prod api_auth
python manage.py makemigrations --settings=ai_draw_plat_v1.settings_prod stable_diffusion
python manage.py makemigrations --settings=ai_draw_plat_v1.settings_prod
python manage.py migrate --settings=ai_draw_plat_v1.settings_prod api_auth
python manage.py migrate --settings=ai_draw_plat_v1.settings_prod stable_diffusion
python manage.py migrate --settings=ai_draw_plat_v1.settings_prod
python manage.py createsuperuser --settings=ai_draw_plat_v1.settings_prod
```

# Project Manager
To manage the project, run:

```bash
supervisord -c  supervisord/supervisord.prod.conf
```
