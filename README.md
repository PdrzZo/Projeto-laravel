<a href="https://laravel.com/"><img src="https://cdn.discordapp.com/attachments/1125487567257739356/1125950651155881984/1200px-Laravel.svg_preview_rev_1.png" width=180 height=100 ></a>  <a href="https://laravel.com/"><img src="https://laravel.com/img/logotype.min.svg" width=200 height=100 ></a> 

<h1> Trabalho para Conclusão da Disciplina Criação de API Rest Básica com PHP</h1>

Professor João Vitor da Costa Andrade

Criação de API Rest básica com PHP e um banco de dados MySQL

- Listar todas as tarefas/GET.

- Detalhes da tarefa específica/GET.

- Adiciona nova tarefa/POST.

- Atualiza dados da tarefa/PUT.

- Excluir tarefa específica/DEL.

- Alguns apps usados:

<a href="https://www.php.net//"><img src="https://cdn.discordapp.com/attachments/1125487567257739356/1125957411862216794/68747470733a2f2f656e637279707465642d74626e302e677374617469632e636f6d2f696d616765733f713d74626e3a414e64394763533459586a70347178316c2d474242447a486d36717572417a64312d7762567354385f7726757371703d434155_preview_rev_1.png" width=180 height=100 ></a> <a href="https://code.visualstudio.com/"><img src="https://cdn.discordapp.com/attachments/1125487567257739356/1125953674926112778/channels4_profile_preview_rev_1.png" width=180 height=100 ></a>  <a href="https://www.postman.com/"><img src="https://cdn.discordapp.com/attachments/1125487567257739356/1125957038367854612/postman-como-instalar-dar-seus-primeiros-passos_preview_rev_1.png" width=300 height=100 ></a>  <a href="https://www.mysql.com/"><img src="https://cdn.discordapp.com/attachments/1125487567257739356/1125957941309214730/MySQL-Logo_preview_rev_1.png" width=200 height=100 ></a> 

<h2> Intruções de como fazer o Sistema de API</h2> 

- Abra o git bash e de um "git clone" do URL do repositório do projeto-laravel do Professor João, após isso de um "cd projeto-laravel/" para poder entrar na pasta e ainda no git bash de o comando "code .".

- Após ter dado o "code .", irá abrir o vscode com todos os códigos já, você irá alterar apenas os seguintes códigos:
<details>
  <summary>app/Http/Controllers/TaskController.php</summary>
  <br/>
 
 ```
 <?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Task;

class TaskController extends Controller
{
    public function index()
    {
        $tasks = Task::all();

        return response()->json($tasks);
    }

    public function show($id)
    {
        $task = Task::find($id);

        if ($task) {
            return response()->json($task);
        } else {
            return response()->json(['error' => 'Tarefa não encontrada'], 404);
        }
    }

    public function store(Request $request)
    {
        $request->validate([
            'title' => 'required',
            'description' => 'required',
        ]);

        $task = new Task;
        $task->title = $request->input('title');
        $task->description = $request->input('description');
        $task->status = $request->input('status', false);
        $task->save();

        return response()->json($task, 201);
    }

    public function update(Request $request, $id)
    {
        $task = Task::find($id);

        if ($task) {
            $request->validate([
                'title' => 'required',
                'description' => 'required',
            ]);

            $task->title = $request->input('title');
            $task->description = $request->input('description');
            $task->status = $request->input('status', $task->status);
            $task->save();

            return response()->json($task);
        } else {
            return response()->json(['error' => 'Tarefa não encontrada'], 404);
        }
    }

    public function destroy($id)
    {
        $task = Task::find($id);

        if ($task) {
            $task->delete();

            return response()->json(['message' => 'Tarefa excluída com sucesso']);
        } else {
            return response()->json(['error' => 'Tarefa não encontrada'], 404);
        }
    }
}
 ```

  </div>
</details> 

<details>
  <summary>database/migrations/2023_06_27_221132_create_tasks_table.php</summary>
  <br/>
 
 ```
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateTasksTable extends Migration
{
    public function up()
    {
        Schema::create('tasks', function (Blueprint $table) {
            $table->id();
            $table->string('title');
            $table->text('description');
            $table->boolean('status')->default(false);
            $table->timestamps();
        });
    }

    public function down()
    {
        Schema::dropIfExists('tasks');
    }
}
 ```

  </div>
</details> 

<details>
  <summary>routes/api.php</summary>
  <br/>
 
 ```
<?php

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Route;

Route::get('/tasks', 'TaskController@index');
Route::get('/tasks/{id}', 'TaskController@show');
Route::post('/tasks', 'TaskController@store');
Route::put('/tasks/{id}', 'TaskController@update');
Route::delete('/tasks/{id}', 'TaskController@destroy');
 ```

  </div>
</details> 


<details>
  <summary>routes/web.php</summary>
  <br/>
 
 ```
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\TaskController;

Route::get('/tasks', [TaskController::class, 'index']);
Route::get('/tasks/{id}', [TaskController::class, 'show']);
Route::post('/tasks', [TaskController::class, 'store']);
Route::put('/tasks/{id}', [TaskController::class, 'update']);
Route::delete('/tasks/{id}', [TaskController::class, 'destroy']);



 ```


  </div>
</details> 

- Após isso copie e cole o ".env.example" novamente e renomeie apenas para ".env", abra o terminal apertando "CTRL+' " e insira "composer install" para poder baixar as dependências do projeto, inicie no XAMPP e de start no Apache e MySQL.
  
- Ainda no terminal insire "php artisan migrate" e "php artisan serve" para poder iniciar o server.
  
- Depois disso é abrir o Postman e criar uma new collection e add resquest para poder criar as funções, após isso é só seguir os passos do vídeo abaixo sobre o Postman.

<h2> Clique na imagem do Youtube para ter o acesso do vídeo:</h2>
<a href="https://www.youtube.com/watch?v=78AuzBKcoyM"><img src="https://cdn.discordapp.com/attachments/1125487567257739356/1125959772022255657/yt_1200_preview_rev_1.png" width=300 height=200 ></a> 
                                                         
https://www.youtube.com/watch?v=78AuzBKcoyM
----
