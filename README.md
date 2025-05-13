# Laravel project setup for new


#New project 
Remember to start up XAMMP with both "Apache" & "MySQL"

For starting a new laravel project go to the terminal and write "laravel new [insert project name]"

after that beofre the project can begin it needs to be connected to the database so run the following command and it will make the database out from your project
"php artisan migrate"

Now you should be able to go into your website within 
http://localhost/dashboard/[project name]/public/

And database is within 
http://localhost/phpmyadmin/



#Commands while working 
Thees commands are meant for when everything is sat up and your are ready to beign your code adventure

##Create a new table 
Makes a modle as well as a controller for the model
php artisan make:model [model name] -mcr
m = to create a model
c = to create a controller
r = to add resource to the contorller file

now in databse/migrations will there be a date form when youn made the model and it contain a schemnatic over the tabel when you are going to migrate it here change it to what is needed and id will be a primary key from the start 
examble 
$table->id();
$table->string('title');
$table->text('content');
$table->timestamps();

Now you should be able to migrate with command below and it will now be added to your database ps remember to refresh your database if you dont see it 
php artisan migrate

then before we can create a post within the model you have created you need to specify what can get postet to the db of info so in this case it would be 
protected $fillable = ['title', 'content']

##CRUD
https://laravel.com/docs/11.x/controllers
So if we need to use CRUD we need to do a few things before we can begin first we need to prepare a route for 

Inside our web.php we need to make it create routes for all of our resource operations within the controller like index, edit, destroy ect.
so we dont need to do them all eventuelt.
use App\Http\Controllers\[Controller name];
Route::resource('[table name]', [Controller name]::class);

Now laravel has thees methods allready so we dont have to make them our self we just need to fokus on giving them info and make sure to send what we get back to our view all of thees are found within the model we made earlier
All()
Find()
Create()
Update()
Delete()

We can call 

