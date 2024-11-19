<details>
<Summary><b>ASSIGNMENT 7</b></summary>

 ### 1. Question: Explain what are stateless widgets and stateful widgets, and explain the difference between them.

Answer: In Flutter, widgets are fundamental components that create the app's user interface, and they are classified into two categories: stateless widgets and stateful widgets. Stateless widgets are immutable, meaning they don’t hold any state that can change over time; their properties are fixed at the time of creation and remain constant throughout the lifecycle of the widget. This makes them ideal for displaying static content, such as text or icons. Conversely, stateful widgets are dynamic and can maintain internal state that may change in response to user interactions or other events, allowing them to rebuild and reflect those changes in the UI. For instance, stateful widgets are often used for interactive elements like forms, checkboxes, or animations. The primary distinction between the two lies in their ability to manage state: stateless widgets rely solely on the data passed to them, while stateful widgets encapsulate both the widget's configuration and the mutable state, enabling a responsive and interactive user experience.

 ### 2. Question: Mention the widgets that you have used for this project and its uses.

 Answer: In this app, StatelessWidget is used in components like MyHomePage, InfoCard, and ItemCard to build elements that don’t need to change once displayed. The whole app is wrapped in MaterialApp, setting up themes, routing, and a consistent design. Each screen layout is managed by Scaffold, providing a base structure with an AppBar at the top for titles and actions, a body, and other essential elements like a floating action button. Spacing and alignment are handled by widgets such as Padding, SizedBox, Center, Column, and Row, allowing you to stack, center, or arrange items both vertically and horizontally.

To display information, Text widgets are used for content, while GridView organizes ItemCard widgets in a scrollable grid format. Card components are also used to give a polished look to items with shadows and a slight elevation, while Material and InkWell add interaction effects like ripples when tapped. For visual icons, Icon provides customizable symbols, and SnackBar shows temporary messages at the screen's bottom for quick feedback, like confirming actions. Finally, Container is a versatile box that holds other widgets and helps manage styling, size, and layout adjustments across different parts of the app.

### 3. Question: What is the use-case for setState()? Explain the variable that can be affected by setState().

 Answer: In Flutter, setState() is utilized within StatefulWidgets to signal that the internal state of the widget has changed, prompting a rebuild of the widget. For example, if there is a variable like int counter = 0 that tracks the number of times a button has been pressed, calling setState(() { counter++; }) increments the counter and updates the UI with the new value. Essentially, any variable defined in the state class that affects the widget's appearance or behavior can be modified using setState().
 
### 4. Question: Explain the difference between const and final keyword.

 Answer: In Dart, the final keyword is used to declare a variable that can be assigned only once, allowing its value to be determined at runtime, whereas const declares a compile time constant that must be known and fixed at compile time. While both prevent reassignment after initialization, final keyword is suitable for values assigned during program execution, such as results from a function, while const is reserved for values that are constant throughout the program and can be used to create constant instances of classes.

### 5. Question: Explain how you implemented the checklist above step-by-step.
Answer:

First I generated a new Flutter project in the terminal with the name nakama_collective, then enter the project directory using this code.

```
flutter create nakama_collective
cd nakama_collective
```

Then I run the project with flutter run and performed the git init, as well as the git add-commit-push to a new GitHub repository. After that, I created a new file named menu.dart and did some modifications until the code looks like this:


```
import 'package:flutter/material.dart';

class MyHomePage extends StatelessWidget {
    MyHomePage({super.key});
    final String npm = '2306173435'; // NPM
    final String name = 'Serafina Nala Putri Setiawan'; // Name
    final String className = 'PBP KKI'; // Class
    final List<ItemHomepage> items = [
    ItemHomepage("View Product List", Icons.list),
    ItemHomepage("Add Product", Icons.add),
    ItemHomepage("Logout", Icons.logout),
     ];
  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".


  @override
   @override
  Widget build(BuildContext context) {
    // Scaffold provides the basic structure of the page with the AppBar and body.
    return Scaffold(
      // AppBar is the top part of the page that displays the title.
      appBar: AppBar(
        title: const Text(
          'Nakama Collective',
          style: TextStyle(
            color: Colors.white,
            fontWeight: FontWeight.bold,
          ),
        ),
        // The background color of the AppBar is obtained from the application theme color scheme.
        backgroundColor: Theme.of(context).colorScheme.primary,
      ),
      // Body of the page with paddings around it.
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        // Place the widget vertically in a column.
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.center,
          children: [
            // Row to display 3 InfoCard horizontally.
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                InfoCard(title: 'NPM', content: npm),
                InfoCard(title: 'Name', content: name),
                InfoCard(title: 'Class', content: className),
              ],
            ),

            // Give a vertical space of 16 units.
            const SizedBox(height: 16.0),

            // Place the following widget in the center of the page.
            Center(
              child: Column(
                // Place the text and grid item vertically.

                children: [
                  // Display the welcome message with bold font and size 18.
                  const Padding(
                    padding: EdgeInsets.only(top: 16.0),
                    child: Text(
                      'Welcome to Nakama Collective',
                      style: TextStyle(
                        fontWeight: FontWeight.bold,
                        fontSize: 18.0,
                      ),
                    ),
                  ),

                  // Grid to display ItemCard in a 3 column grid.
                  GridView.count(
                    primary: true,
                    padding: const EdgeInsets.all(20),
                    crossAxisSpacing: 10,
                    mainAxisSpacing: 10,
                    crossAxisCount: 3,
                    // To ensure that the grid fits its height.
                    shrinkWrap: true,

                    // Display ItemCard for each item in the items list.
                    children: items.map((ItemHomepage item) {
                      return ItemCard(item);
                    }).toList(),
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}


class InfoCard extends StatelessWidget {
  // Card information that displays the title and content.

  final String title;  // Card title.
  final String content;  // Card content.

  const InfoCard({super.key, required this.title, required this.content});

  @override
  Widget build(BuildContext context) {
    return Card(
      // Create a card box with a shadow.
      elevation: 2.0,
      child: Container(
        // Set the size and spacing within the card.
        width: MediaQuery.of(context).size.width / 3.5, // Adjust with the width of the device used.
        padding: const EdgeInsets.all(16.0),
        // Place the title and content vertically.
        child: Column(
          children: [
            Text(
              title,
              style: const TextStyle(fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 8.0),
            Text(content),
          ],
        ),
      ),
    );
  }
}


class ItemHomepage {
    final String name;
    final IconData icon;

    ItemHomepage(this.name, this.icon);
}


class ItemCard extends StatelessWidget {
  // Display the card with an icon and name.

  final ItemHomepage item; 
  
  const ItemCard(this.item, {super.key}); 

  @override
  Widget build(BuildContext context) {
    // Set color based on the item name
    Color backgroundColor;
    if (item.name == "View Product List") {
      backgroundColor = Colors.green;
    } else if (item.name == "Add Product") {
      backgroundColor = Colors.yellow;
    } else if (item.name == "Logout") {
      backgroundColor = Colors.red;
    } else {
      backgroundColor = Theme.of(context).colorScheme.secondary;
    }

    return Material(
      color: backgroundColor, // Apply the background color
      borderRadius: BorderRadius.circular(12),
      
      child: InkWell(
        onTap: () {
          // Display the SnackBar message when the card is pressed.
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(
              SnackBar(content: Text("You have pressed the ${item.name} button!"))
            );
        },
        child: Container(
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

Following along, I did some modifications to main.dart until the file looks like this:

```
import 'package:flutter/material.dart';
import 'package:nakama_collective/menu.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Nakama Collective',
      theme: ThemeData(
        // This is the theme of your application.
        //
        // TRY THIS: Try running your application with "flutter run". You'll see
        // the application has a purple toolbar. Then, without quitting the app,
        // try changing the seedColor in the colorScheme below to Colors.green
        // and then invoke "hot reload" (save your changes or press the "hot
        // reload" button in a Flutter-supported IDE, or press "r" if you used
        // the command line to start the app).
        //
        // Notice that the counter didn't reset back to zero; the application
        // state is not lost during the reload. To reset the state, use hot
        // restart instead.
        //
        // This works for code too, not just values: Most code changes can be
        // tested with just a hot reload.
         colorScheme: ColorScheme.fromSwatch(
       primarySwatch: Colors.deepPurple,
 ).copyWith(secondary: Colors.deepPurple[400]),
      ),
      home: MyHomePage(),
    );
  }
}
```
Finally, I performed the add, commit, and push to update the GitHub repository.
</details>

<details>
<Summary><b>ASSIGNMENT 8</b></summary>

### 1. Question : What is the purpose of const in Flutter? Explain the advantages of using const in Flutter code. When should we use const, and when should it not be used?
Answer: In Flutter, the const keyword is used to define objects that are immutable and determined at compile time, making them an essential tool for optimizing performance in Flutter apps. By marking widgets or values as const, they become reusable, allowing Flutter to avoid recreating these objects during rebuilds, which reduces memory usage and improves rendering efficiency. This is particularly useful for widgets with static content, such as icons or text, that remain constant throughout the app's lifecycle. However, const should not be used for dynamic content or values that depend on runtime data, as they require mutability and cannot be determined at compile time. The key advantage of const is its ability to streamline the app’s performance by minimizing unnecessary object creation, making it ideal for building efficient and scalable UIs.

### 2. Question : Explain and compare the usage of Column and Row in Flutter. Provide example implementations of each layout widget!
Answer: In Flutter, Column and Row are essential layout widgets used to arrange child widgets in a linear fashion, but they differ in orientation. A Column arranges its children vertically, from top to bottom, making it ideal for stacking elements like a list or form. In contrast, a Row places its children horizontally, from left to right, which is often used for layouts like navigation bars or toolbars. Both widgets offer alignment controls, such as mainAxisAlignment for positioning along the primary axis and crossAxisAlignment for the secondary axis, allowing flexibility in design. For example, a Column could display text labels stacked vertically, while a Row might align icons and text side by side. The choice between the two depends on whether the layout needs to be vertical or horizontal, making them indispensable tools for building organized and responsive UIs.

### 3. Question : List the input elements you used on the form page in this assignment. Are there other Flutter input elements you didn’t use in this assignment? Explain!
Answer: In this assignment, the form page incorporates several input elements to collect product details. I utilized TextFormField widgets for various inputs, including the product name, description, price, and quantity. The product name and description fields accept strings, allowing users to provide textual information about the product. The price and quantity fields are also implemented as TextFormField widgets, with validation to ensure that the inputs are valid numbers, making sure the data entered is accurate and appropriate for the respective fields. 

There are other Flutter input elements that weren't used in this assignment like Checkbox that could be used for binary choices, Radio buttons for selecting one option from a group, Switch for toggling between two states, and DropdownButton for selecting an item from a list. 

### 4. Question : How do you set the theme within a Flutter application to ensure consistency? Did you implement a theme in your application?
Answer:  In my main.dart, I used the ThemeData class to customize the theme. Specifically, I created a color scheme using ColorScheme.fromSwatch, where I selected Colors.teal as the primary color and Colors.teal[400] for the secondary color. This means the main elements of my app, like the app bar, buttons, and other UI components, will follow this color palette.

### 5. Question : How do you manage navigation in a multi-page Flutter application?
Answer: In a multi page Flutter application, navigation is managed using the Navigator class, which handles the stack of pages or screens. The basic approach involves using Navigator.push() to navigate to a new screen and Navigator.pop() to return to the previous one. For more structured and organized navigation, especially in larger apps, named routes are commonly used. This allows you to define route names in the MaterialApp widget and navigate using Navigator.pushNamed(). Additionally, side menus like Drawer and bottom navigation bars can be implemented by pushing new routes based on user interactions. For complex navigation needs, libraries like go_router or auto_route offer advanced routing features, enabling nested navigation and easier management of page transitions. 

</details>

<details>
<Summary><b>ASSIGNMENT 9</b></summary>

### Question 1: Explain why we need to create a model to retrieve or send JSON data. Will an error occur if we don't create a model first? 
Answer: Creating a model to handle JSON data helps organize and validate the data before sending or retrieving it. Without a model, the data can be messy and inconsistent, leading to errors or unexpected behavior. While you can send or receive JSON without a model, it’s riskier because you lose the structure and checks that a model provides, which can lead to issues like corrupted data or bad responses. A model makes sure everything is in order and reduces the chance of errors.

### Question 2: Explain the function of the http library that you implemented for this task.
Answer: The http library in Flutter is used to send requests between the Flutter app and the Django backend. It allows the app to fetch data from or send data to the Django API using methods like GET and POST. For example, a GET request can retrieve data, while a POST request sends information such as user input. The library also helps handle responses, manage errors, and include authentication tokens in headers when needed.
 
### Question 3: Explain the function of CookieRequest and why it’s necessary to share the CookieRequest instance with all components in the Flutter app.
Answer: The CookieRequest class in Flutter is used to manage cookies, which help maintain user sessions or store authentication data. When a user logs in, the server sends a cookie, and this cookie needs to be included in future requests. Sharing the CookieRequest instance across the app is important because it ensures that the same cookie is sent with every request, keeping the user's session active. If the instance isn't shared, different parts of the app might treat the user as a new session, leading to issues like being logged out unexpectedly.
 
### Question 4: Explain the mechanism of data transmission, from input to display in Flutter.
Answer: In Flutter, when a user inputs data (like typing in a text field or tapping a button), it gets stored in the app's state. The app can then process this data, such as sending it to a server or making changes locally. Once the data is updated, Flutter automatically refreshes the UI to show the new information. This ensures that the display always reflects the latest state, whether it's based on user input or data fetched from a backend.

### Question 5: Explain the authentication mechanism from login, register, to logout. Start from inputting account data in Flutter to Django’s completion of the authentication process and display of the menu in Flutter.
Answer: The authentication process begins in Flutter when the user enters their account details in the login or registration form. Flutter sends this data to the Django backend via an HTTP request. In the case of registration, Django creates a new user account and sends a success response. For login, Django checks the credentials, and if they’re correct, it returns a token. Flutter stores this token securely to keep the user logged in. On logout, the token is removed. After successful authentication, Django sends back the necessary data and Flutter updates the UI to show the menu or user-specific content.

### Question 6: Explain how you implement the checklist above step by step! (not just following the tutorial).
Answer: 

First I set up authentication in django for Flutter by creating a django app named authentication in my nakama-collective django and added authentication to INSTALLED_APPS in the main project settings.py file of the django application. Then I run the command ```pip install django-cors-headers``` to install the required library after enabling the virtual environment and adding django-cors-headers to ```requirements.txt``` as well. After that I aaded corsheaders to INSTALLED_APPS in the main project settings.py file in the nakama-collective django and added
```corsheaders.middleware.CorsMiddleware``` to MIDDLEWARE in the ```settings.py``` of the main project.  

To integrate the Flutter Form with the Django Service, I created a new views function in the main/views.py in the Django project. Then I connected the page product_form.dart to CookieRequest by adding this code 

```
@csrf_exempt
def create_product_flutter(request):
    if request.method == 'POST':

        data = json.loads(request.body)
        new_product = Product.objects.create(
            user=request.user,
            name=data["name"],
            description=data["description"],
            price=int(data["price"]),
            stock=int(data["stock"]),
        )

        new_product.save()

        return JsonResponse({"status": "success"}, status=200)
    else:
        return JsonResponse({"status": "error"}, status=401)
```
I also connected the page productentry_form.dart to CookieRequest by adding this code.

```
@override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();

    return Scaffold(

```
For logout feature implementation, I added a method for logout in the authentication/views.py

```
@csrf_exempt
def logout(request):
    username = request.user.username

    try:
        auth_logout(request)
        return JsonResponse({
            "username": username,
            "status": True,
            "message": "Logged out successfully!"
        }, status=200)
    except:
        return JsonResponse({
        "status": False,
        "message": "Logout failed."
        }, status=401)
```
Then to create a detail page for each item listed on the Product list page, I created a new file product_details.dart which consists of this

```
import 'package:flutter/material.dart'; 
import 'package:nakama_collective/models/product_entry.dart'; 
class ProductDetailsPage extends StatelessWidget {
  final Product product;
  const ProductDetailsPage({super.key, required this.product});
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(product.fields.name), 
        centerTitle: true,
        actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.chevron_left),
            onPressed: () => Navigator.pop(context), 
          ),
        ], // Widget[]
      ), // AppBar
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              product.fields.name,
              style: const TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
            ), // Text
            const SizedBox(height: 10),
            Text("Description: ${product.fields.description}", style: const TextStyle(fontSize: 16)),
            const SizedBox(height: 10),
            Text("Price: ${product.fields.price}", style: const TextStyle(fontSize: 16)),
            const SizedBox(height: 10),
            Text("Stock: ${product.fields.stock}", style: const TextStyle(fontSize: 16)),
          ],
        ),
      ),
    );
  }
}
```

Then in list_productentry.dart I imported the product_details.dart

```

import 'package:nakama_collective/widgets/product_details.dart';

```

Next I added these lines

```
 title: const Text('Product List'),
        backgroundColor: Theme.of(context).colorScheme.primary,
        foregroundColor: Colors.white,
```
```
itemBuilder: (context, index) {
                  final product = snapshot.data![index];
                  return InkWell(
                    onTap: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (context) => ProductDetailsPage(product: product),
                        ),
                      );
                    },
                    child: Card(
                      margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
                      child: Container(
                        decoration: BoxDecoration(
                          border: Border.all(
                            color: Colors.grey, // Color of the border
                            width: 1, // Width of the border
                          ),
                          borderRadius: BorderRadius.circular(12), // Border radius of the container
                        ),
                        padding: const EdgeInsets.all(20.0),
                        child: Column(
                          mainAxisAlignment: MainAxisAlignment.start,
                          crossAxisAlignment: CrossAxisAlignment.start,
                          children: [
                            Text(
                              "${snapshot.data![index].fields.name}",
                              style: const TextStyle(
                                fontSize: 18.0,
                                fontWeight: FontWeight.bold,
                              ),
                            ),
                            const SizedBox(height: 10),
                            Text("${snapshot.data![index].fields.description}"),
                            const SizedBox(height: 10),
                            Text("${snapshot.data![index].fields.price}"),
                            const SizedBox(height: 10),
                            Text("${snapshot.data![index].fields.stock}")
                          ],
```

</details>