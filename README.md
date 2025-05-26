# Laravel project setup for new
Follow good guide use it for first time download or messed something up like deleting xammp and downloading it to another folder
https://www.youtube.com/watch?v=iBaM5LYgyPk

# Cloning of laravel
So sadly noting will work as it should when getting the project to a new device but for that you should run thees commands 
* npm i
* composer i
* php artisan key:generate (Create your env file first before running this command)(it's used for encryption and decryption so remember to save it in some place or else)

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


# Model & Controller
So laravel is build on model, controller and view where model is for the database and controller to share databse info with the view.
for that reason we need to build a model before we can make a controller

So to create a model we will use this command<br/><br/>
**REMEMBER model names need to be in PascalCase!!!!!**<br/>
"php artisan make:model [model name]" -mcrfs

* m = to create a migration file
* c = to create a controller
* r = adds resource to the contorller file ('creates method for controller to talk to the model of manupulations or getting of data')

* f = to create a factoris file ('create mass random data need to be used with seed')
* s = to create a seed file ('sends data to database auto')


## Model
For models it controlls the database for what data is alowed in and out 

Her is an examble of protection agenst mass asignment ('sends array of data to the db') it will help project with only being able to be sendt/ update only thess three rows in the db will be able while if there are others inputs thats not in view will be delt within laravel such as id feks. <br/> <br/>
protected $fillable = ['name', 'password', 'email'];<br/><br/>

There is also another way to improve securite like using an arrow with attributes like type or rquired something that could be change in the view so it helps where it wont be able to be just changed<br/> <br/>
protected $fillable = [
  'name' => 'required|string|max:255',
  'email' => 'required|email|unique:users',
];<br/>

## Controller
Controller helps for the data we ask from our model

## Migration
With migration this will help to build your database

Here is an examble of on schema of the table i wish to be created in my database<br/>
Here we can se that it will **create an id, product_name, price, quantity and timestamps that create created_at and updated_at**<br/><br/>

we simply say what type they contain and we can also give them more informaiton sutch as a **nullable()** to say they are allowed to be empty
and we dont really need to say id is primary with auto generation sense it already know that itself so most of the work can be done on its own regard <br/><br/>

Schema::create('storage_items', function (Blueprint $table) {<br/>
  $table->id();<br/>
  $table->string('product_name')->default('');<br/>
  $table->integer('price');<br/>
  $table->integer('quantity')->nullable();<br/>
  $table->timestamps();<br/>
});<br/><br/>

*php artisan migrate ('to upload the tables into your database')

## Factories
With factories we build data formats that will be send to our database so we dont have to do it all manually <br/>
We do go back to our **Migation file** to see what it needs and use them we use someting like

* fake ('to say false information/ random')
* word/name/city ('add one of thees like name if it was a user we wanted to create')

 return [<br/>
  'product_name' => fake()->word(),<br/>
  'price' => fake() -> numberBetween(100, 10000),<br/>
  'quantity' => fake() -> numberBetween(1, 100),<br/>
  'created_at' => now(),<br/>
  'updated_at' => now(),<br/>
];<br/>

## Seeders
In  our seeders we then get to call our **Factories** or we can create our own data and send up if its something specific <br/><br/>

Here is an examble with **Factories** <br/> 
With this we will need to call our model that will find the factorie for us with its own models 
and within the function in the run we call our model and creates with the amount we want in this examble 50 that when run will creatre them all in the db when its done 

use App\Models\StorageItem;<br/>

public function run(): void <br/>
{StorageItem::factory()->count(50)->create(); }<br/><br/>


In this examble we dont need to call our model to find our factories sense it doesnt exist insted we can hard code what roles need to be created and only thees data will be sendt to the db<br/>

public function run(): void <br/>
{  Role::create([   'role' => 'Employee', ]); <br/>
Role::create([ 'role' => 'Manager',]); } <br/><br/>

And the one thing you will need to do is put them all in the file called DatabaseSeeder sense it's the only file to be ran buy a specifc command  <br/>
it will call the other seed classes you have made just becarful when using forign keys then you might want to structur them a bit diffrent <br/>

 $this->call([<br/>
   RoleSeeder::class<br/>
   UserSeeder::class<br/>
   StorageItemSeeder::class,<br/>
]);<br/>



### RUN Seed
For running the seed you should call this in the terminal<br/>
**php artisan db:seed** <br/><br/>

There is also other ways to do it if you also want to fix some bugs or updates migration or even delete all data<br/>

* make:reset ('Removes all tables in the database exept migration')
* make:fresh ('Combinds with removeing all tables and makes add them in again')
* --seed ('To send data best used with **make:fresh**')


## Routing
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

