
  
# Introduction 

## What is Airflow?
Apache Airflow is an **open-source tool to programmatically author, schedule, and monitor workflows**. It is mostly used for orchestrating workflows or pipelines. You can easily visualize your data pipelines' dependencies, progress, logs, code, trigger tasks, and success status.
[Documentation](https://airflow.apache.org/docs/apache-airflow/stable/)

![The advantages of intelligent warehouse management - Mecalux.com](https://mecaluxcom.cdnwm.com/logistics-items/the-advantages-of-intelligent-warehouse-management/image-0.1.1.jpg)

## How is it useful? 
1. Airflow makes **it easy to monitor the state of a pipeline in their UI**.
2.  You can build DAGs with complex fan-in and fan-out relationships between tasks
3. They also add: “Rich command line utilities make performing complex surgeries on DAGs a snap.”
4. Airflow is a Warehouse Management System (WMS) **that defines tasks and and their dependencies as code**, executes those tasks on a regular schedule, and distributes task execution across worker processes.
![Image](https://miro.medium.com/max/1200/1*czjWSmrjiRY1goA0emv7IA.png)

## What is DAG?
1. In Airflow, a DAG – or a Directed Acyclic Graph – is **a collection of all the tasks you want to run**, organized in a way that reflects their relationships and dependencies.  Here's a basic example DAG:
![dag example](https://progressivecoder.com/wp-content/uploads/2021/07/dag-example.png)
2. It defines four Tasks - A, B, C, and D - and dictates the order in which they have to run, and which tasks depend on what others. It will also say how often to run the DAG - maybe "every 5 minutes starting tomorrow", or "every day since January 1st, 2020".
3. The DAG itself doesn't care about _what_ is happening inside the tasks; it is merely concerned with _how_ to execute them - the order to run them in, how many times to retry them, if they have timeouts, and so on.

> Note: The below example is not a **DAG**:  

![](https://progressivecoder.com/wp-content/uploads/2021/07/not-a-dag.png)  

4. A valid **DAG** can execute in an **Airflow installation**. Whenever, a DAG is triggered, a DAGRun is created. We can think of a **DAGrun** as an instance of the DAG with an execution timestamp.

## What are Nodes in a DAG?
A Node is nothing but an operator.

To elaborate, an operator is a class that contains the logic of what we want to achieve in the DAG. For example, if we want to execute a Python script, we will have a  **Python operator**. If we wish to execute a Bash command, we have  **Bash operator**. There are several in-built operators available to us as part of Airflow. Documentation about them can be found  [here](https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/operators/index.html).

When a particular operator is triggered, it becomes a task and executes as part of the overall DAG run.

## Principles

-   **Dynamic**: Airflow pipelines are configuration as code (Python), allowing for dynamic pipeline generation. This allows for writing code that instantiates pipelines dynamically.
    
-   **Extensible**: Easily define your own operators, executors and extend the library so that it fits the level of abstraction that suits your environment.
    
-   **Elegant**: Airflow pipelines are lean and explicit. Parameterizing your scripts is built into the core of Airflow using the powerful  **Jinja**  templating engine.
    
-   **Scalable**: Airflow has a modular architecture and uses a message queue to orchestrate an arbitrary number of workers. Airflow is ready to scale to infinity.
# Installing Airflow

## Running from samagra/airflow docker image
> Requirement: Docker
1. In order to use Airflow in click to run state we have dockerised a version of our airflow in our own template format. You can download it from [here](https://github.com/Samagra-Development/airflow)
2. [OPTIONAL]: Set up any   **secrets management tool specifically designed to control access to sensitive credentials in a low-trust environment** if you have any in the .env file in the project root directory.
	> In our case we are using HashiCorp Vault  

3. Then go to terminal/command prompt and run the following command to run the airflow with default configs and user.
```shell
docker-compose -f docker-compose-CeleryExecutor.yml up -d
```
4. Create a folder named dags inside project directory. *This is the default path to store your dags*
	>**Root Folder Structure:**
	```bash
	.
    ├── .dockerignore
    ├── .gitignore
    ├── Dockerfile
    ├── LICENSE
    ├── README.md
    ├── config
    │   └── airflow.cfg
    ├───dags
    ├── docker-compose-CeleryExecutor.yml
    ├── docker-compose-LocalExecutor.yml
    ├── requirements.txt
    ├── sample.env
    └── script
        └── entrypoint.sh	
    ```
5. You can check the aiflow ui running on http://localhost:8181
	> default username and password: admin,admin


## Other Installation Methods

-   [Using released sources](https://airflow.apache.org/docs/apache-airflow/stable/installation/index.html#using-released-sources)
    
-   [Using PyPI](https://airflow.apache.org/docs/apache-airflow/stable/installation/index.html#using-pypi)
    
-   [Using Production Docker Images](https://airflow.apache.org/docs/apache-airflow/stable/installation/index.html#using-production-docker-images)
    
-   [Using Official Airflow Helm Chart](https://airflow.apache.org/docs/apache-airflow/stable/installation/index.html#using-official-airflow-helm-chart)
    
-   [Using Managed Airflow Services](https://airflow.apache.org/docs/apache-airflow/stable/installation/index.html#using-managed-airflow-services)
    
-   [Using 3rd-party images, charts, deployments](https://airflow.apache.org/docs/apache-airflow/stable/installation/index.html#using-3rd-party-images-charts-deployments)

## Airflow UI
When workflows are defined as code, they become more maintainable, versionable, testable, and collaborative.

![_images/airflow.gif](https://airflow.apache.org/docs/apache-airflow/stable/_images/airflow.gif)

# Using Airflow

## Creating a DAG

> **Requirements:** Exposure with python and its syntax
### Create a Hello World DAG
Assuming that Airflow is already setup, we will create our first  _hello world_  DAG. All it will do is print a message to the log.
Below is the code for the DAG.
```python
from datetime import datetime
from airflow import DAG
from airflow.operators.dummy_operator import DummyOperator
from airflow.operators.python_operator import PythonOperator

def print_hello():
    return 'Hello world from first Airflow DAG!'

dag = DAG('hello_world', description='Hello World DAG',
          schedule_interval='0 12 * * *',
          start_date=datetime(2017, 3, 20), catchup=False)

hello_operator = PythonOperator(task_id='hello_task', python_callable=print_hello, dag=dag)

hello_operator
```
* We place this code (DAG) in our **AIRFLOW_HOME** directory under the **dags** folder. We name it _hello_world.py_.
```bash
	.
    ├── .dockerignore
    ├── .gitignore
    ├── Dockerfile
    ├── LICENSE
    ├── README.md
    ├── config
    │   └── airflow.cfg
    ├───dags
    │   └── hello_world.py
    ├── docker-compose-CeleryExecutor.yml
    ├── docker-compose-LocalExecutor.yml
    ├── requirements.txt
    ├── sample.env
    └── script
        └── entrypoint.sh	
   ```
   
   Let us understand what we have done in the file:

*   In the first few lines, we are simply importing a few packages from  **airflow**.
*   Next, we define a function that prints the hello message.
*   After that, we declare the DAG. It takes arguments such as  **name**,  **description**,  **schedule_interval**,  **start_date**  and  **catchup**. Setting catchup to false prevents Airflow from having the DAG runs catch up to the current date.
* Check more on how to write cron expressions for schedule_interval [here](https://airflow.apache.org/docs/apache-airflow/1.10.1/scheduler.html)
*   Next, we define the operator and call it the  **hello_operator**. In essence, this uses the in-built  **PythonOperator** to call our  **print_hello**  function. We also provide a task_id to this operator.
*   The last statement specifies the order of the operators. In this case, we have only one operator.

### Running the DAG
To run the DAG, we need to start the  **Airflow scheduler**  by executing the below command:

```
airflow scheduler
```

**Airflow scheduler**  is the entity that actually executes the DAGs.  We are ruuning our airflow on **CeleryExecutor** which executes tasks by scaling up workers. In case of more complex workflow, we can use other executors such as  **LocalExecutor** or  **SequentialExecutor**.

If we have the  **Airflow webserver**  also running, we would be able to see our  **hello_world**  DAG in the list of available DAGs.

![](https://progressivecoder.com/wp-content/uploads/2021/07/airflow_dag_list-1024x142.png)

To start the DAG, we can to turn on the DAG by clicking the toggle button before the name of the DAG. As soon as that is done, we would be able to see messages in the scheduler logs about the DAG execution.

```
[2021-07-03 11:49:16,962] {scheduler_job.py:1212} INFO - Executor reports execution of hello_world.hello_task execution_date=2021-07-01 12:00:00+00:00 exited with status success for try_number 1
[2021-07-03 11:49:17,100] {dagrun.py:444} INFO - Marking run <DagRun hello_world @ 2021-07-01 12:00:00+00:00: scheduled__2021-07-01T12:00:00+00:00, externally triggered: False> successful
```

We can also see the DAG graph view where the  **hello_world**  operator has executed successfully.

[![airflow dag graph view](https://progressivecoder.com/wp-content/uploads/2021/07/airflow_dag_graph_view-1024x363.png)](https://progressivecoder.com/wp-content/uploads/2021/07/airflow_dag_graph_view.png)

By clicking on the task box and opening the logs, we can see the logs as below:

```
[2021-07-03 11:49:16,755] {python.py:151} INFO - Done. Returned value was: Hello world from first Airflow DAG!
[2021-07-03 11:49:16,768] {taskinstance.py:1191} INFO - Marking task as SUCCESS. dag_id=hello_world, task_id=hello_task, execution_date=20210701T120000, start_date=20210703T061916, end_date=20210703T061916
[2021-07-03 11:49:16,781] {taskinstance.py:1245} INFO - 0 downstream tasks scheduled from follow-on schedule check
[2021-07-03 11:49:16,820] {local_task_job.py:151} INFO - Task exited with return code 0
```

Here, we can see the hello world message. In other words, our DAG executed successfully and the task was marked as SUCCESS.

----------

With this  **Airflow DAG Example**, we have successfully created our first DAG and executed it using Airflow. Though it was a simple hello message, it has helped us understand the concepts behind a DAG execution in detail.

## Creating your first Airflow DAG

There are **4 steps** to follow to create a data pipeline. Don’t forget, your goal is to code the following DAG:
![](https://docs.google.com/drawings/d/e/2PACX-1vSd4yb0GPj43lHeSomVj5c6bGYy8nmzZZ9j20I7_c_C4DifGvOe_41BN0oqVS6jDPAPm-8n2pNEaHWj/pub?w=1130&h=404)

Without further do, let’s begin!

#### Step 1: Make the Imports

The first step is to import the classes you need. To create a DAG in Airflow, you always have to import the DAG class. After the DAG class, come the imports of Operators. Basically, for each Operator you want to use, you have to make the corresponding import. For example, you want to execute a Python function, you have to import the PythonOperator. You want to execute a bash command, you have to import the BashOperator. Finally, the last import is usually the datetime class as you need to specify a start date to your DAG.

```python
from airflow import DAG
from airflow.operators.python import PythonOperator, BranchPythonOperator
from airflow.operators.bash import BashOperator
from datetime import datetime
```

#### Step 2: Create the Airflow DAG object

After having made the imports, the second step is to create the Airflow DAG object. A DAG object must have two parameters, a  _dag_id_  and a  _start_date_. The dag_id is the  **unique identifier**  of the DAG across all of DAGs. Each DAG must have a unique  _dag_id_. The  _start_date_  defines  **the date at which your DAG starts being scheduled**. Warning here,

**If the start_date is set in the past, the scheduler will try to backfill all the non-triggered DAG Runs between the  _start_date_  and the current date.**  For example, if your  _start_date_  is defined with a date 3 years ago, you might end up with many DAG Runs running at the same time.

In addition those arguments, 2 others are usually specified. The  _schedule_interval_  and the  _catchup_  arguments.

The  _schedule_interval_  defines **the interval of time at which your DAG gets triggered**. Every 10 mins, every day, every month and so on. 2 ways to define it, either with a CRON expression or with a timedelta object. The first option is the most often used. By the way, if you don’t know how to define a CRON expression, take a look at this beautiful  [website](https://crontab.guru/)  and if you don’t know what a CRON expression is, keep in mind that it is way to express time intervals.

Lastly, the  _catchup_  argument allows you to prevent from backfilling automatically the non triggered DAG Runs between the start date of your DAG and the current date. If you want don’t want to end up with many DAG runs running at the same time, it’s usually a best practice to set it to False.

That’s it, no more arguments and here is the corresponding code,

```python
with DAG("my_dag", # Dag id
start_date=datetime(2021, 1 ,1), # start date, the 1st of January 2021 
schedule_interval='@daily',  # Cron expression, here it is a preset of Airflow, @daily means once every day.
catchup=False  # Catchup 
) as dag:
```

Notice that to create an instance of a DAG, we use the with statement. Why? Because “with” is a context manager and allows you to better manager objects. In that case, a DAG object. I won’t go into the details here but I advise you to instantiate your DAGs like that. It’s clearer and better than creating a variable and put your DAG into.

#### Step 3: Add your tasks!

Once you have made the imports and created your DAG object, you are ready to add your tasks! Remember, a task is an operator. Therefore, based on your DAG, you have to add 6 operators. Let’s dive into the tasks.

##### **Training model tasks**

First, training model A, B and C, are implemented with the PythonOperator. Since we are not going to train real machine learning models (too complicated to start), each task will return a random accuracy. This accuracy will be generated from a python function named _training_model.

```python
from random import randint # Import to generate random numbers
def _training_model():
return randint(1, 10) # return an integer between 1 - 10
with DAG(...) as dag:
# Tasks are implemented under the dag object
training_model_A = PythonOperator(
task_id="training_model_A",
python_callable=_training_model
)
training_model_B = PythonOperator(
task_id="training_model_B",
python_callable=_training_model
)
training_model_C = PythonOperator(
task_id="training_model_C",
python_callable=_training_model
)

```


##### **Choosing best model**

The next task is “Choosing Best ML”. Since this task executes either the task “accurate” or “inaccurate” based on the best accuracy, the BranchPythonOperator looks like to be the perfect candidate for that. It allows you to execute one task or another based on a condition, a value, a criterion. If you want to learn more about it, take a look  [here](https://marclamberti.com/blog/airflow-branchpythonoperator/). The BranchPythonOperator is one of the most commonly used Operator, so don’t miss it.

How to implement it? Here is the answer,

```python
def _choosing_best_model(ti):
accuracies = ti.xcom_pull(task_ids=[
'training_model_A',
'training_model_B',
'training_model_C'
])
if max(accuracies) > 8:
return 'accurate'
return 'inaccurate'
with DAG(...) as dag:
choosing_best_model = BranchPythonOperator(
task_id="choosing_best_model",
python_callable=_choosing_best_model
)
```

Ok, it looks a little bit more complicated here. Let’s start by the beginning. First, the BranchPythonOperator executes a python function. Here, _choosing_best_model. This function must return the task id of the next task to execute. For your DAG, either “accurate” or “inaccurate” as shown from the return keywords. Now, there is something we didn’t talk about yet. What is xcom_pull? 😱

Whenever you want to share data between tasks in Airflow, you have to use XCOMs. XCOM stands for cross-communication messages, it is a mechanism allowing to exchange small data between the tasks of a DAG. A XCOM is an object encapsulating a key, serving as an identifier, and a value, corresponding to the value you want to share. I won’t go into the details here as I made a long  [article](https://marclamberti.com/blog/airflow-xcom/)  about it, just keep in mind that by returning the accuracy from the python function _training_model_X, we create a XCOM with that accuracy, and with xcom_pull in _choosing_best_model, we fetch that XCOM back corresponding to the accuracy. As we want the accuracy of each training_model task, we specify the task ids of these 3 tasks. That’s all you need to know 😃

##### **Accurate or inaccurate?**

The last two tasks to implements are “accurate” and “inaccurate”. To do that, you can use the BashOperator and execute a very simple bash command to either print “accurate” or “inaccurate” on the standard output.

```python
accurate = BashOperator(
task_id="accurate",
bash_command="echo 'accurate'"
)
inaccurate = BashOperator(
task_id="inaccurate",
bash_command=" echo 'inaccurate'"
)
```

That’s it, nothing more to add. The BashOperator is used to execute bash commands and that’s exactly what you’re doing here.

All right, that was a lot, time to move to the last step!

#### Step 4: Defining dependencies

Now you’ve implemented all of the tasks, the last step is to put the glue between them or in other words, to define the dependencies between them. How? By using bitshift operators.

In your case, it’s really basic as you want to execute one task after the other.

```python
 with DAG(...) as dag:
training_model_tasks >> choosing_best_model >> [accurate, inaccurate]
```

Here you say that  _training_model_tasks_  are executed first, then once all of the tasks are completed,  _choosing_best_model_  gets executed, and finally, either  _accurate_  or  _inaccurate_. Keep in mind that each time you have multiple tasks that should be on the same level, in a same group, that can be executed at the same time, use a list with [ ].

#### The Final Airflow DAG!

Ok, now you’ve gone through all the steps, time to see the final code:

```python
from airflow import DAG
from airflow.operators.python import PythonOperator, BranchPythonOperator
from airflow.operators.bash import BashOperator
from datetime import datetime
from random import randint
def _choosing_best_model(ti):
accuracies = ti.xcom_pull(task_ids=[
'training_model_A',
'training_model_B',
'training_model_C'
])
if max(accuracies) > 8:
return 'accurate'
return 'inaccurate'
def _training_model(model):
return randint(1, 10)
with DAG("my_dag",
start_date=datetime(2021, 1 ,1), 
schedule_interval='@daily', 
catchup=False) as dag:
training_model_tasks = [
PythonOperator(
task_id=f"training_model_{model_id}",
python_callable=_training_model,
op_kwargs={
"model": model_id
}
) for model_id in ['A', 'B', 'C']
]
choosing_best_model = BranchPythonOperator(
task_id="choosing_best_model",
python_callable=_choosing_best_model
)
accurate = BashOperator(
task_id="accurate",
bash_command="echo 'accurate'"
)
inaccurate = BashOperator(
task_id="inaccurate",
bash_command=" echo 'inaccurate'"
)
training_model_tasks >> choosing_best_model >> [accurate, inaccurate]
```

That’s it you’ve just created your first Airflow DAG! If you want to test it, put that code into a file my_dag.py and put that file into the folder dags/ of Airflow. Once you’ve done that, run it from the UI and you should obtain the following output:

![](https://marclamberti.com/wp-content/uploads/Screenshot-2021-03-02-at-22.43.28.png)


> You can schedule talend jobs from airflow too. Here is an example of adding talend jobs as tasks using BashOperator.
```python
from datetime import datetime
from airflow import DAG
from airflow.operators.dummy_operator import DummyOperator
from airflow.operators.python_operator import PythonOperator

dag = DAG('hello_world', description='Hello World DAG', schedule_interval='0 12 * * *', start_date=datetime(2017,  3,  20), catchup=False) 

insert_data = BashOperator(  
    task_id='using_bash_opertor',  
  bash_command='<folder path where talend export is present>/<script file> ',  
  retries=3,  
  dag=dag)
  
  insert_data 
```rking task as SUCCESS. dag_id=hello_world, task_id=hello_task, execution_date=20210701T120000, start_date=20210703T061916, end_date=20210703T061916
[2021-07-03 11:49:16,781] {taskinstance.py:1245} INFO - 0 downstream tasks scheduled from follow-on schedule check
[2021-07-03 11:49:16,820] {local_task_job.py:151} INFO - Task exited with return code 0
```

Here, we can see the hello world message. In other words, our DAG executed successfully and the task was marked as SUCCESS.

----------

With this  **Airflow DAG Example**, we have successfully created our first DAG and executed it using Airflow. Though it was a simple hello message, it has helped us understand the concepts behind a DAG execution in detail.

## Creating your first Airflow DAG

There are **4 steps** to follow to create a data pipeline. Don’t forget, your goal is to code the following DAG:
![](https://docs.google.com/drawings/d/e/2PACX-1vSd4yb0GPj43lHeSomVj5c6bGYy8nmzZZ9j20I7_c_C4DifGvOe_41BN0oqVS6jDPAPm-8n2pNEaHWj/pub?w=1130&h=404)

Without further do, let’s begin!

#### Step 1: Make the Imports

The first step is to import the classes you need. To create a DAG in Airflow, you always have to import the DAG class. After the DAG class, come the imports of Operators. Basically, for each Operator you want to use, you have to make the corresponding import. For example, you want to execute a Python function, you have to import the PythonOperator. You want to execute a bash command, you have to import the BashOperator. Finally, the last import is usually the datetime class as you need to specify a start date to your DAG.

```python
from airflow import DAG
from airflow.operators.python import PythonOperator, BranchPythonOperator
from airflow.operators.bash import BashOperator
from datetime import datetime
```

#### Step 2: Create the Airflow DAG object

After having made the imports, the second step is to create the Airflow DAG object. A DAG object must have two parameters, a  _dag_id_  and a  _start_date_. The dag_id is the  **unique identifier**  of the DAG across all of DAGs. Each DAG must have a unique  _dag_id_. The  _start_date_  defines  **the date at which your DAG starts being scheduled**. Warning here,

**If the start_date is set in the past, the scheduler will try to backfill all the non-triggered DAG Runs between the  _start_date_  and the current date.**  For example, if your  _start_date_  is defined with a date 3 years ago, you might end up with many DAG Runs running at the same time.

In addition those arguments, 2 others are usually specified. The  _schedule_interval_  and the  _catchup_  arguments.

The  _schedule_interval_  defines **the interval of time at which your DAG gets triggered**. Every 10 mins, every day, every month and so on. 2 ways to define it, either with a CRON expression or with a timedelta object. The first option is the most often used. By the way, if you don’t know how to define a CRON expression, take a look at this beautiful  [website](https://crontab.guru/)  and if you don’t know what a CRON expression is, keep in mind that it is way to express time intervals.

Lastly, the  _catchup_  argument allows you to prevent from backfilling automatically the non triggered DAG Runs between the start date of your DAG and the current date. If you want don’t want to end up with many DAG runs running at the same time, it’s usually a best practice to set it to False.

That’s it, no more arguments and here is the corresponding code,

```python
with DAG("my_dag", # Dag id
start_date=datetime(2021, 1 ,1), # start date, the 1st of January 2021 
schedule_interval='@daily',  # Cron expression, here it is a preset of Airflow, @daily means once every day.
catchup=False  # Catchup 
) as dag:
```

Notice that to create an instance of a DAG, we use the with statement. Why? Because “with” is a context manager and allows you to better manager objects. In that case, a DAG object. I won’t go into the details here but I advise you to instantiate your DAGs like that. It’s clearer and better than creating a variable and put your DAG into.

#### Step 3: Add your tasks!

Once you have made the imports and created your DAG object, you are ready to add your tasks! Remember, a task is an operator. Therefore, based on your DAG, you have to add 6 operators. Let’s dive into the tasks.

##### **Training model tasks**

First, training model A, B and C, are implemented with the PythonOperator. Since we are not going to train real machine learning models (too complicated to start), each task will return a random accuracy. This accuracy will be generated from a python function named _training_model.

```python
from random import randint # Import to generate random numbers
def _training_model():
return randint(1, 10) # return an integer between 1 - 10
with DAG(...) as dag:
# Tasks are implemented under the dag object
training_model_A = PythonOperator(
task_id="training_model_A",
python_callable=_training_model
)
training_model_B = PythonOperator(
task_id="training_model_B",
python_callable=_training_model
)
training_model_C = PythonOperator(
task_id="training_model_C",
python_callable=_training_model
)

```

That’s great but you can do better. Indeed, the 3 tasks are really similar. The only difference lies into the task ids. Therefore, since DAGs are coded in Python, we can benefit from that and generate the tasks dynamically. Take a look at the code below

```python
training_model_tasks = [
PythonOperator(
task_id=f"training_model_{model_id}",
python_callable=_training_model,
op_kwargs={
"model": model_id
}
) for model_id in ['A', 'B', 'C']
]
```

By defining a list comprehension, we are able to generate the 3 tasks dynamically which is…. much cleaner. Less code, the better 😎

If you are wondering how the PythonOperator works, take a look at my article  [here](https://marclamberti.com/blog/airflow-pythonoperator/), you will learn everything you need about it.

##### **Choosing best model**

The next task is “Choosing Best ML”. Since this task executes either the task “accurate” or “inaccurate” based on the best accuracy, the BranchPythonOperator looks like to be the perfect candidate for that. It allows you to execute one task or another based on a condition, a value, a criterion. If you want to learn more about it, take a look  [here](https://marclamberti.com/blog/airflow-branchpythonoperator/). The BranchPythonOperator is one of the most commonly used Operator, so don’t miss it.

How to implement it? Here is the answer,

```python
def _choosing_best_model(ti):
accuracies = ti.xcom_pull(task_ids=[
'training_model_A',
'training_model_B',
'training_model_C'
])
if max(accuracies) > 8:
return 'accurate'
return 'inaccurate'
with DAG(...) as dag:
choosing_best_model = BranchPythonOperator(
task_id="choosing_best_model",
python_callable=_choosing_best_model
)
```

Ok, it looks a little bit more complicated here. Let’s start by the beginning. First, the BranchPythonOperator executes a python function. Here, _choosing_best_model. This function must return the task id of the next task to execute. For your DAG, either “accurate” or “inaccurate” as shown from the return keywords. Now, there is something we didn’t talk about yet. What is xcom_pull? 😱

Whenever you want to share data between tasks in Airflow, you have to use XCOMs. XCOM stands for cross-communication messages, it is a mechanism allowing to exchange small data between the tasks of a DAG. A XCOM is an object encapsulating a key, serving as an identifier, and a value, corresponding to the value you want to share. I won’t go into the details here as I made a long  [article](https://marclamberti.com/blog/airflow-xcom/)  about it, just keep in mind that by returning the accuracy from the python function _training_model_X, we create a XCOM with that accuracy, and with xcom_pull in _choosing_best_model, we fetch that XCOM back corresponding to the accuracy. As we want the accuracy of each training_model task, we specify the task ids of these 3 tasks. That’s all you need to know 😃

##### **Accurate or inaccurate?**

The last two tasks to implements are “accurate” and “inaccurate”. To do that, you can use the BashOperator and execute a very simple bash command to either print “accurate” or “inaccurate” on the standard output.

```python
accurate = BashOperator(
task_id="accurate",
bash_command="echo 'accurate'"
)
inaccurate = BashOperator(
task_id="inaccurate",
bash_command=" echo 'inaccurate'"
)
```

That’s it, nothing more to add. The BashOperator is used to execute bash commands and that’s exactly what you’re doing here.

All right, that was a lot, time to move to the last step!

#### Step 4: Defining dependencies

Now you’ve implemented all of the tasks, the last step is to put the glue between them or in other words, to define the dependencies between them. How? By using bitshift operators.

In your case, it’s really basic as you want to execute one task after the other.

```python
 with DAG(...) as dag:
training_model_tasks >> choosing_best_model >> [accurate, inaccurate]
```

Here you say that  _training_model_tasks_  are executed first, then once all of the tasks are completed,  _choosing_best_model_  gets executed, and finally, either  _accurate_  or  _inaccurate_. Keep in mind that each time you have multiple tasks that should be on the same level, in a same group, that can be executed at the same time, use a list with [ ].

#### The Final Airflow DAG!

Ok, now you’ve gone through all the steps, time to see the final code:

```python
from airflow import DAG
from airflow.operators.python import PythonOperator, BranchPythonOperator
from airflow.operators.bash import BashOperator
from datetime import datetime
from random import randint
def _choosing_best_model(ti):
accuracies = ti.xcom_pull(task_ids=[
'training_model_A',
'training_model_B',
'training_model_C'
])
if max(accuracies) > 8:
return 'accurate'
return 'inaccurate'
def _training_model(model):
return randint(1, 10)
with DAG("my_dag",
start_date=datetime(2021, 1 ,1), 
schedule_interval='@daily', 
catchup=False) as dag:
training_model_tasks = [
PythonOperator(
task_id=f"training_model_{model_id}",
python_callable=_training_model,
op_kwargs={
"model": model_id
}
) for model_id in ['A', 'B', 'C']
]
choosing_best_model = BranchPythonOperator(
task_id="choosing_best_model",
python_callable=_choosing_best_model
)
accurate = BashOperator(
task_id="accurate",
bash_command="echo 'accurate'"
)
inaccurate = BashOperator(
task_id="inaccurate",
bash_command=" echo 'inaccurate'"
)
training_model_tasks >> choosing_best_model >> [accurate, inaccurate]
```

That’s it you’ve just created your first Airflow DAG! If you want to test it, put that code into a file my_dag.py and put that file into the folder dags/ of Airflow. Once you’ve done that, run it from the UI and you should obtain the following output:

![](https://marclamberti.com/wp-content/uploads/Screenshot-2021-03-02-at-22.43.28.png)
