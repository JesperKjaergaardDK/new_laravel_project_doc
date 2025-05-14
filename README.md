# Laravel project setup for new


# New project 
Remember to start up XAMMP with both "Apache" & "MySQL"

For starting a new laravel project go to the terminal and write "laravel new [insert project name]"

After that beofre the project can begin it needs to be connected to the database so run the following command and it will make the database out from your project
"php artisan migrate"

Now you should be able to go into your website within 
http://localhost/dashboard/[project name]/public/ 

you should copi the same path to the .env file so when running the test envirement it goes directly to it 
APP_URL=http://localhost/dashboard/[project name]/public/

And database is within 
http://localhost/phpmyadmin/


# Database help
Thees commands are meant for when everything is sat up and your are ready to beign your code adventure

## Create a new table 
Makes a model as well as a controller for the model <br/>
"php artisan make:model [model name] -mcr"
* m = to create a model
* c = to create a controller
* r = adds resource to the contorller file

Now in databse/migrations folder there will be a file dateed form when you made the model and it contain a schemnatic over the tabel when you are going to migrate into the database. 
examble:

* $table->id();
* $table->string('title');
* $table->text('content');
* $table->timestamps(); 

Now you should be able to migrate with command below and it will now be added to your database ps remember to refresh your database if you dont see it  <br/>
"php artisan migrate"

Then before we can create a request to our database within the specified table the model you have created you need to specify what can get send to the database of information for protection so in this case it would be  <br/>
protected $fillable = ['title', 'content']

## CRUD
https://laravel.com/docs/11.x/controllers <br/>
So if we need to use CRUD we need to do a few things before we can begin first we need to prepare a route for 

Inside our web.php we need to make it create routes for all of our resource operations within the controller like index, edit, destroy ect. but there is a line we could use that says 'Oh i will just make all fetchs just needs to go though me and i will send them to the correct method in the controller' so we dont need to manual create them all individuelle. <br/>

* use App\Http\Controllers\[Controller name];
* Route::resource('[folder name]', [Controller name]::class);

Okay so now the connection to the router is connected you will have to at the view part when you make a form to send a fetch request to the backend about wanting data use lines like
* "{{ route('[route folder name].[controller methods]', [Additionel data transfer]) }}"
* "{{ route('blogs.update', $blog->id) }}

//With in the controller where the methods exist thees are the following commands to contact the databse with
* all()
* find()
* create()
* update()
* delete()
* findOrFail()

In work it would look somehting like this <br/>
$variable = "[Model]::[one of the above]" 

