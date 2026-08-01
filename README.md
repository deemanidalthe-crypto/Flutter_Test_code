# Flutter_Test_code

# Flutter:
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        colorScheme: .fromSeed(seedColor: Colors.deepPurple),
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});
  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: .center,
          children: [
            const Text('You have pushed the button this many times:'),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headlineMedium,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: const Icon(Icons.add),
      ),
    );
  }
}
  _____________________________________________________________________________________________________________________________________________________________
# setting :
  import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

class SettingScreen extends StatefulWidget {
  const SettingScreen({super.key});

  @override
  State<SettingScreen> createState() => _SettingScreenState();
}

class _SettingScreenState extends State<SettingScreen> {
  String username = "Guest";

  @override
  void initState() {
    super.initState();
    getUsername();
  }

  Future<void> getUsername() async {
    final prefs = await SharedPreferences.getInstance();

    setState(() {
      username = prefs.getString("username") ?? "Guest";
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Settings"),
      ),
      body: Center(
        child: Text(
          "Welcome $username",
          style: const TextStyle(
            fontSize: 24,
          ),
        ),
      ),
    );
  }
}
 _______________________________________________________________________________________________________________________________________________________________
# welcom :
import 'package:flutter/material.dart';
import 'package:flutter_application_1/screens/home.dart';
import 'package:shared_preferences/shared_preferences.dart';

class WelcomeScreen extends StatefulWidget {
  const WelcomeScreen({super.key});

  @override
  State<WelcomeScreen> createState() => _WelcomeScreenState();
}

class _WelcomeScreenState extends State<WelcomeScreen> {
  final GlobalKey<FormState> formKey = GlobalKey<FormState>();

  final TextEditingController controller = TextEditingController();

  String name = "";

  @override
  void dispose() {
    controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,

      body: SafeArea(
        child: SingleChildScrollView(
          child: Padding(
            padding: const EdgeInsets.symmetric(
              horizontal: 20,
            ),

            child: Form(
              key: formKey,

              child: Column(
                children: [

                  const SizedBox(height: 55),
                  Row(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [

                      Image.asset(
                        "assets/app.jpg",
                        width: 35,
                        height: 35,
                      ),

                      const SizedBox(width: 10),

                      const Text(
                        "Tasky",
                        style: TextStyle(
                          color: Colors.black,
                          fontSize: 26,
                          fontWeight: FontWeight.w500,
                        ),
                      ),
                    ],
                  ),

                  const SizedBox(height: 70),
                  const Text(
                    "Welcome To Tasky ",
                    style: TextStyle(
                      color: Colors.black,
                      fontSize: 28,
                      fontWeight: FontWeight.bold,
                    ),
                  ),

                  const SizedBox(height: 8),

                  const Text(
                    "Your productivity starts here.",
                    style: TextStyle(
                      color: Colors.blue,
                      fontSize: 15,
                    ),
                  ),

                  const SizedBox(height: 25),
                  Image.asset(
                    "assets/app.jpg",
                    width: 210,
                    height: 210,
                    fit: BoxFit.contain,
                  ),

                  const SizedBox(height: 25),
                  const Align(
                    alignment: Alignment.centerLeft,
                    child: Text(
                      "Full Name",
                      style: TextStyle(
                        color: Colors.black,
                        fontSize: 14,
                      ),
                    ),
                  ),

                  const SizedBox(height: 8),
                  TextFormField(
                    controller: controller,

                    onChanged: (value) {
                      name = value;
                    },

                    validator: (value) {
                      if (value == null || value.trim().isEmpty) {
                        return "Please enter your name";
                      }
                      return null;
                    },

                    style: const TextStyle(
                      color: Colors.white,
                    ),

                    decoration: InputDecoration(
                      hintText: "username",

                      hintStyle: const TextStyle(
                        color: Colors.grey,
                      ),

                      filled: true,
                      fillColor: const Color(0xff242424),

                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(12),
                        borderSide: BorderSide.none,
                      ),

                      enabledBorder: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(12),
                        borderSide: BorderSide.none,
                      ),

                      focusedBorder: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(12),
                        borderSide: const BorderSide(
                          color: Colors.green,
                        ),
                      ),
                    ),
                  ),

                  const SizedBox(height: 20),
                  SizedBox(
                    width: double.infinity,
                    height: 52,

                    child: ElevatedButton(
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.blue,

                        shape: RoundedRectangleBorder(
                          borderRadius: BorderRadius.circular(30),
                        ),
                      ),

                      onPressed: () async {

                        if (formKey.currentState!.validate()) {

                          final prefs =
                          await SharedPreferences.getInstance();

                          await prefs.setString(
                            "username",
                            controller.text,
                          );

                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                              builder: (_) => const HomeScreen(),
                            ),
                          );
                        }
                      },

                      child: const Text(
                        "Let's Get Started",
                        style: TextStyle(
                          color: Colors.white,
                          fontSize: 16,
                        ),
                      ),
                    ),
                  ),

                  const SizedBox(height: 25),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
 ______________________________________________________________________________________________________________________________________________________________
 # sharedprefser
 import 'dart:convert';
import 'package:flutter_application_1/screens/task_modele.dart';
import 'package:shared_preferences/shared_preferences.dart';


class SharedPrefService {
  static const String taskKey = "tasks";

  static Future<void> saveTasks(List<TaskModel> tasks) async {
    final prefs = await SharedPreferences.getInstance();
    List<Map<String, dynamic>> taskList =
    tasks.map((task) => task.toJson()).toList();

    String jsonString = jsonEncode(taskList);
    await prefs.setString(taskKey, jsonString);
  }

  static Future<List<TaskModel>> getTasks() async {
    final prefs = await SharedPreferences.getInstance();

    String? jsonString = prefs.getString(taskKey);
    if (jsonString == null) {
      return [];
    }

    List decodedData = jsonDecode(jsonString);
    return decodedData
        .map((task) => TaskModel.fromJson(task))
        .toList();
  }
}
________________________________________________________________________________________________________________________________________________________________
# add :
 import 'package:flutter/material.dart';
import 'package:flutter_application_1/SharedPrefSer.dart';
import 'package:flutter_application_1/screens/task_modele.dart';
class AddTaskScreen extends StatefulWidget {
  const AddTaskScreen({super.key});

  @override
  State<AddTaskScreen> createState() => _AddTaskScreenState();
}

class _AddTaskScreenState extends State<AddTaskScreen> {
  final GlobalKey<FormState> formKey = GlobalKey<FormState>();
  final TextEditingController titleController = TextEditingController();

  final TextEditingController descriptionController =
  TextEditingController();

  bool isHighPriority = false;

  @override
  void dispose() {
    titleController.dispose();
    descriptionController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {

    return Scaffold(
      backgroundColor: Colors.white,
      appBar: AppBar(
        backgroundColor: Colors.white,
        elevation: 0,

        title: const Text(
          "New Task",
          style: TextStyle(
            color: Colors.black,
            fontWeight: FontWeight.bold,
          ),
        ),

        iconTheme: const IconThemeData(
          color: Colors.black,
        ),
      ),

      body: Form(
        key: formKey,

        child: Padding(
          padding: const EdgeInsets.all(20),

          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,

            children: [

      
              const Text(
                "Task Name",
                style: TextStyle(
                  fontWeight: FontWeight.w600,
                ),
              ),

              const SizedBox(height: 10),

              TextFormField(

                controller: titleController,

                validator: (value){

                  if(value==null || value.trim().isEmpty){
                    return "Please Enter Task Name";
                  }

                  return null;

                },

                decoration: InputDecoration(

                  hintText: "Enter task name",

                  filled: true,

                  fillColor: Colors.grey.shade100,

                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(15),
                  ),
                ),
              ),

              const SizedBox(height: 25),
              const Text(
                "Description",
                style: TextStyle(
                  fontWeight: FontWeight.w600,
                ),
              ),

              const SizedBox(height: 10),

              TextFormField(

                controller: descriptionController,

                maxLines: 4,

                validator: (value){

                  if(value==null || value.trim().isEmpty){
                    return "Please Enter Description";
                  }

                  return null;

                },

                decoration: InputDecoration(

                  hintText: "Task description",

                  filled: true,

                  fillColor: Colors.grey.shade100,

                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(15),
                  ),
                ),
              ),

              const SizedBox(height: 25),
              Row(

                mainAxisAlignment: MainAxisAlignment.spaceBetween,

                children: [

                  const Text(
                    "High Priority",
                    style: TextStyle(
                      fontSize: 16,
                      fontWeight: FontWeight.w500,
                    ),
                  ),

                  Switch(

                    value: isHighPriority,

                    activeColor: Colors.blue,

                    onChanged: (value){

                      setState(() {

                        isHighPriority = value;

                      });

                    },
                  )
                ],
              ),

              const Spacer(),
              SizedBox(

                width: double.infinity,

                height: 55,

                child: ElevatedButton(

                  style: ElevatedButton.styleFrom(

                    backgroundColor: Colors.blue,

                    shape: RoundedRectangleBorder(

                      borderRadius: BorderRadius.circular(30),

                    ),
                  ),

                  onPressed: () async {

                    if (formKey.currentState!.validate()) {
                      TaskModel task = TaskModel(
                        title: titleController.text,
                        description: descriptionController.text,
                        isHighPriority: isHighPriority,
                      );
                      List<TaskModel> tasks =
                      await SharedPrefService.getTasks();
                      tasks.add(task);
                      await SharedPrefService.saveTasks(tasks);
                      Navigator.pop(context);
                    }
                  },

                  child: const Text(

                    "Add Task",

                    style: TextStyle(

                      color: Colors.white,

                      fontSize: 16,

                    ),
                  ),
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
 _______________________________________________________________________________________________________________________________________________________________
# model :

class TaskModel {
  
  String title;

  String description;
  bool isCompleted;
  bool isHighPriority;

  TaskModel({
    required this.title,
    required this.description,
    this.isCompleted = false,
    this.isHighPriority = false,
  });
    Map<String, dynamic> toMap() {
    return {
      "title": title,
      "description": description,
      "isCompleted": isCompleted,
      "isHighPriority": isHighPriority,
    };
  }

    factory TaskModel.fromMap(Map<String, dynamic> map) {
    return TaskModel(
      title: map["title"],
      description: map["description"],
      isCompleted: map["isCompleted"],
      isHighPriority: map["isHighPriority"],
    );
  }
  Map<String, dynamic> toJson() {
    return toMap();
  }
  factory TaskModel.fromJson(Map<String, dynamic> json) {
    return TaskModel.fromMap(json);
  }
}
 ___________________________________________________________________________________________________________________________________________________________
 # main :
 import 'package:flutter/material.dart';
import 'package:flutter_application_1/screens/welcom.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: const HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: WelcomeScreen(),
    );
  }
}
 _________________________________________________________________________________________________________________________________________________________________
 # home :
 import 'package:flutter/material.dart';
import 'package:flutter_application_1/SharedPrefSer.dart';
import 'package:flutter_application_1/screens/add.dart';
import 'package:flutter_application_1/screens/task_modele.dart';

class HomeScreen extends StatefulWidget {

  const HomeScreen({super.key});


  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  List<TaskModel> tasks = [];
  @override
  void initState() {
    super.initState();
    loadTasks();
  }
  Future<void> loadTasks() async {
    tasks = await SharedPrefService.getTasks();
    setState(() {});
  }
  @override
  Widget build(BuildContext context) {
    return Scaffold(

      backgroundColor: Colors.white,
      appBar: AppBar(
        backgroundColor: Colors.white,
        elevation: 0,
        centerTitle: false,

        title: const Text(
          "Tasky",
          style: TextStyle(
            color: Colors.black,
            fontWeight: FontWeight.bold,
          ),
        ),

        actions: [

          Padding(
            padding: const EdgeInsets.only(right: 15),

            child: CircleAvatar(
              radius: 18,
              backgroundColor: Colors.blue,

              child: const Icon(
                Icons.person,
                color: Colors.white,
              ),
            ),
          )
        ],
      ),
      body: Padding(
        padding: const EdgeInsets.all(20),

        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,

          children: [
            const Text(
              "Good Evening ",
              style: TextStyle(
                fontSize: 16,
                color: Colors.grey,
              ),
            ),

            const SizedBox(height: 5),

            const Text(
              "One task at a time One step closer.",
              style: TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
              ),
            ),

            const SizedBox(height: 35),

            const Text(
              "Today's Tasks",
              style: TextStyle(
                fontSize: 20,
                fontWeight: FontWeight.w600,
              ),
            ),

            const SizedBox(height: 20),

        Expanded(
          child: tasks.isEmpty
              ? Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  Icons.task_alt,
                  size: 80,
                  color: Colors.grey.shade300,
                ),
                const SizedBox(height: 15),
                const Text(
                  "No Tasks Yet",
                  style: TextStyle(
                    fontSize: 22,
                    fontWeight: FontWeight.bold,
                  ),
                ),
                const SizedBox(height: 8),
                const Text(
                  "Press the button below\nand add your first task.",
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    color: Colors.grey,
                  ),
                ),
              ],
            ),
          )
              : ListView.builder(
            itemCount: tasks.length,
            itemBuilder: (context, index) {
              TaskModel task = tasks[index];

              return Dismissible(
                key: Key(task.description + index.toString()),

                background: Container(
                  alignment: Alignment.centerRight,
                  padding: const EdgeInsets.only(right: 20),
                  color: Colors.red,

                  child: const Icon(
                    Icons.delete,
                    color: Colors.white,
                  ),
                ),

                onDismissed: (_) async {

                  setState(() {
                    tasks.removeAt(index);
                  });

                  await SharedPrefService.saveTasks(tasks);

                  ScaffoldMessenger.of(context).showSnackBar(
                    const SnackBar(
                      content: Text("Task Deleted"),
                    ),
                  );
                },

                child: Card(
                  margin: const EdgeInsets.only(bottom: 15),

                  child: ListTile(

                    title: Text(task.title),

                    subtitle: Text(task.description),

                    trailing: Checkbox(
                      value: task.isCompleted,
                      onChanged: (value) async {

                        setState(() {
                          task.isCompleted = value!;
                        });

                        await SharedPrefService.saveTasks(tasks);
                      },
                    ),
                  ),
                ),
              );
            },
          ),
        ),
          ],
        ),
      ),
       floatingActionButton: FloatingActionButton.extended(

        backgroundColor: Colors.blue,

        onPressed: () async{

          await Navigator.push(
            context,
            MaterialPageRoute(
              builder: (context) => const  AddTaskScreen(),
            ),
          );
          loadTasks();

        },

        icon: const Icon(
          Icons.add,
          color: Colors.white,
        ),

        label: const Text(
          "New Task",
          style: TextStyle(
            color: Colors.white,
          ),
        ),
      ),
    );
  }
}
