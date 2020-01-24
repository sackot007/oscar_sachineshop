1. Create Virtual Env named “oscar_eshop”
virtualenv --python=python3 oscar_eshop 

2. Activate Virtual Env
source ./oscar_eshop/bin/activate

2.1(OPTIONAL) To Deactivate and Remove Virtual Env
deactivate {while on (oscar_eshop) prompt}
rm -r oscar_eshop

3. Install OSCAR into the VirtualEnv
pip install django-oscar

4. Start and initialize the project named “sachineshop”
django-admin.py startproject sachineshop

5. Above step would create a folder named “sachineshop”. Edit settings.py and urls.py as in this dir.
 
6. Load above settings to the DB
python3 manage.py migrate

7. Note: You may get an error “ModuleNotFoundError: No module named 'sorl'”. Install sorl
pip install sorl-thumbnail

8. Re-run migrate command
python3 manage.py migrate

9. Run server.
python3 manage.py runserver
Note: Site runs on http://127.0.0.1:8000/ and admin console path is http://127.0.0.1:8000/admin/

10. Set superuser for admin console
python3 manage.py createsuperuser

11. To install all country codes
pip install pycountry 

12. Pouplate all countries to Oscar dashboard. Note: --no-shipping doesn't select any default country.
python manage.py oscar_populate_countries --no-shipping




======================================================================================================

====================================== For Physical Stores ======================================

On Ubuntu, install following packages. We use spatialite library for Geo mapping.

sudo apt-get install spatialite-bin libspatialite7 libgeos++-dev libgdal-dev libproj9
sudo apt-get install libsqlite3-mod-spatialite

pip install  pysqlite3
pip install django-oscar-stores

python3 manage.py collectstatic -- To collect django-oscar-stores static files

In settings.py, add the following for Google Map API key and search distance
==========================================

INSTALLED_APPS = [
	.......,
	'stores',
    'stores.dashboard',
	........,
]
.........
# Modified sqlite3 to spatialite.
DATABASES = {
    'default': {
        'ENGINE': 'django.contrib.gis.db.backends.spatialite',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
.........
GOOGLE_MAPS_API_KEY = '***********[ENTER_UR_KEY]'
.........
from django.contrib.gis.measure import D

# Maximal distance of 25 kilometers
STORES_MAX_SEARCH_DISTANCE = D(km=25)


In urls.py, add the following
==========================================
	path('stores/',apps.get_app_config('stores').urls),
    path('dashboard/stores/', apps.get_app_config('stores_dashboard').urls),
