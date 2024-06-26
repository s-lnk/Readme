# Laravel notes

## Setting livewire 3.x with Laravel 11.x - configure update endpoint
If using custom path for domain i.e. c:\xampp\htdocs\MYPROJ\, set custom endpoint \vendor\livewire\livewire\src\LivewireServiceProvider.php
```
use Illuminate\Support\Facades\Route;
```
And update boot function to contain setUpdateRoute
```
    public function boot()
    {
        $this->bootMechanisms();
        $this->bootFeatures();
		Livewire::setUpdateRoute(function ($handle) {
			return Route::post('/MYPROJ/livewire/update', $handle);
		});
    }
```
