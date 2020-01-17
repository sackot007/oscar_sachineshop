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
