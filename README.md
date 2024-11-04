 ASSIGNMENT 7

 1. Question: Explain what are stateless widgets and stateful widgets, and explain the difference between them.

Answer: In Flutter, widgets are fundamental components that create the app's user interface, and they are classified into two categories: stateless widgets and stateful widgets. Stateless widgets are immutable, meaning they don’t hold any state that can change over time; their properties are fixed at the time of creation and remain constant throughout the lifecycle of the widget. This makes them ideal for displaying static content, such as text or icons. Conversely, stateful widgets are dynamic and can maintain internal state that may change in response to user interactions or other events, allowing them to rebuild and reflect those changes in the UI. For instance, stateful widgets are often used for interactive elements like forms, checkboxes, or animations. The primary distinction between the two lies in their ability to manage state: stateless widgets rely solely on the data passed to them, while stateful widgets encapsulate both the widget's configuration and the mutable state, enabling a responsive and interactive user experience.

 2. Question: Mention the widgets that you have used for this project and its uses.

 Answer: 
- StatelessWidget
Usage: MyHomePage, InfoCard, ItemCard, MyApp
Purpose: Used for building widgets that do not hold any mutable state. They can be rebuilt when their parent widget changes.
- MaterialApp
Usage: In MyApp
Purpose: The top-level widget that wraps the entire application and provides the necessary context for material design. It sets up themes, routing, and other app-wide configurations.
- Scaffold
Usage: In MyHomePage
Purpose: Provides a framework that implements the basic material design visual layout structure, including the AppBar, body, FloatingActionButton, BottomNavigationBar, etc.
- AppBar
Usage: In MyHomePage
Purpose: A material design app bar that holds the title and other actions at the top of the screen.
- Padding
Usage: In MyHomePage
Purpose: A widget that adds empty space around its child. Useful for providing space between widgets to improve layout and appearance.
- Column
Usage: In MyHomePage
Purpose: A widget that arranges its children vertically. It allows developers to stack multiple widgets on top of each other.
- Row
Usage: In MyHomePage
Purpose: Similar to Column, but arranges its children horizontally. Used to display InfoCard widgets side by side.
- SizedBox
Usage: In MyHomePage
Purpose: A box with a specified size, used to create vertical space between widgets.
- Center
Usage: In MyHomePage
Purpose: A widget that centers its child within itself. Useful for aligning widgets in the middle of the screen.
- Text
Usage: In InfoCard and MyHomePage
Purpose: A widget that displays a string of text with a single style. It's customizable for font size, weight, color, and alignment.
- GridView
Usage: In MyHomePage
Purpose: A scrollable grid that displays its children in a two-dimensional array. Used here to display the ItemCard widgets in a grid layout.
- Card
Usage: In InfoCard and ItemCard
Purpose: A material design card that provides a surface for displaying information. It has a shadow effect and can contain other widgets.
- Material
Usage: In ItemCard
Purpose: A widget that provides a Material design visual effect. Used to apply the background color and elevation to the ItemCard.
- InkWell
Usage: In ItemCard
Purpose: A material design widget that responds to touch events, allowing for tap gestures. It provides ripple effects when tapped.
- Icon
Usage: In ItemCard
Purpose: A widget that displays an icon. Icons can be customized in size and color.
- SnackBar
Usage: In ItemCard
Purpose: A lightweight message that provides feedback about an operation. It appears temporarily at the bottom of the screen.
- Container
Usage: In various widgets
Purpose: A box model that can contain other widgets, allowing for size, padding, alignment, decoration, and constraints. Used for layout adjustments and styling.

 3. Question: What is the use-case for setState()? Explain the variable that can be affected by setState().

 Answer: In Flutter, setState() is utilized within StatefulWidgets to signal that the internal state of the widget has changed, prompting a rebuild of the widget. For example, if there is a variable like int counter = 0 that tracks the number of times a button has been pressed, calling setState(() { counter++; }) increments the counter and updates the UI with the new value. Essentially, any variable defined in the state class that affects the widget's appearance or behavior can be modified using setState().
 
 4. Question: Explain the difference between const and final keyword.

 Answer: In Dart, the final keyword is used to declare a variable that can be assigned only once, allowing its value to be determined at runtime, whereas const declares a compile time constant that must be known and fixed at compile time. While both prevent reassignment after initialization, final keyword is suitable for values assigned during program execution, such as results from a function, while const is reserved for values that are constant throughout the program and can be used to create constant instances of classes.

5. Question: Explain how you implemented the checklist above step-by-step.
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