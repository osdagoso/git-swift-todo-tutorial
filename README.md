# Tutorial de aplicación de lista de tareas en Swift

## IMPORTANT

This tutorial is the Spanish translation of @jadekler's original tutorial to help teach latinamerican students about the basics of Swift.

=======================

_Note:_ This repo is fairly out of date. Use at your own risk.

CODE version: xCode 7.2.1, Swift 2.0

README version: xCode 6.0, Swift 1.0

=======================

- [Preámbulo](#user-content-preámbulo)
- [Instalando la aplicación](#user-content-instalando-la-aplicación)
- [Retroalimentación](#user-content-retroalimentación)
- [Introducción](#user-content-introducción)
  - [Crea tu proyecto](#user-content-crea-tu-proyecto)
  - [Agrega un campo de texto al storyboard](#user-content-agrega-un-campo-de-texto-al-storyboard)
- [Uniendo nuestras vistas: The storyboard](#user-content-uniendo-nuestras-vistas-the-storyboard)
  - [Posicionando el campo de texto utilizando Auto Layout](#user-content-posicionando-el-campo-de-texto-utilizando-auto-layout)
  - [Crear un table view controller](#user-content-crear-un-controlador-de-table-view)
  - [Agregar un ‘segue’ para navegar hacia adelante](#user-content-agregar-un-segue-para-navegar-hacia-adelante)
  - [Configurar el botón de agregar](#user-content-configurar-el-botón-de-agregar)
  - [Agregar un controlador de navegación al controlador de view](#user-content-agregar-un-controlador-de-navegación-al-controlador-de-view)
- [Finally Programming: Swift](#user-content-finally-programming-swift)
  - [Create a custom view controller that is a subclass of UIViewController](#user-content-create-a-custom-view-controller-that-is-a-subclass-of-uiviewcontroller)
  - [Create a custom table view controller that is a subclass of UITableViewController](#user-content-create-a-custom-table-view-controller-that-is-a-subclass-of-uitableviewcontroller)
  - [Connecting cancel and done buttons to exit segue](#user-content-connecting-cancel-and-done-buttons-to-exit-segue)
  - [Create a Data Class](#user-content-create-a-data-class)
  - [Fill in your TodoItem class](#user-content-fill-in-your-todoitem-class)
  - [Give your table view controller an array of TodoItems](#user-content-give-your-table-view-controller-an-array-of-todoitems)
  - [Marcar elemento completado](#user-content-marcar-elemento-completado)
  - [Por último - agregar nuevos elementos](#user-content-por-ultimo---agregar-nuevos-elementos)

## Preámbulo

1. Este tutorial es una versión actualizada y en español del [Swift TODO App Tutorial](https://github.com/jadekler/git-swift-todo-tutorial) de jadekler.
1. El tutorial de jadekler está basado en el [Tutorial TODO en Objective C para Xcode 5 de Apple](https://developer.apple.com/library/ios/referencelibrary/GettingStarted/RoadMapiOS/index.html#//apple_ref/doc/uid/TP40011343-CH2-SW1), el cual es una excelente referencia para buscar recursos adicionales y capturas de pantalla.
1. En el folder Todo encontrarás el código de la aplicación terminada en caso de que lo necesites.

## Instalando la aplicación

1. `cd /tu/directorio/de/xcode`
1. `git clone https://github.com/jadekler/git-swift-todo-tutorial.git`
1. Abre Xcode
1. Archivo > Abrir > /tu/directorio/de/xcode/git-swift-todo-tutorial/Todo/Todo.xcodeproj

## Retroalimentación

¡Cualquier pregunta, sugerencia o retroalimentación es bienvenida! Contáctame a través de mi correo electrónico: osdagoso@hotmail.com.

## Introducción

##### Crea tu proyecto
1. Abre Xcode
1. En la barra de menú, ve a iOS > Application, selecciona 'Single View Application' y haz click en Next
1. Ingresa lo siguiente: ![](/img/img_1.png)
1. Presiona el botón de ejecutar en la esquina superior izquierda de xCode - ahora debe aparecer una pantalla en blanco

##### Agrega un campo de texto al storyboard
1. En el Project Navigator, ubicado en la columna izquierda de xCode, selecciona Main.storyboard
1. Localiza la Object Library en la parte inferior de la columna derecha y escribe en la barra de búsqueda 'Text Field'
1. <img src="https://raw.githubusercontent.com/jadekler/git-swift-todo-tutorial/updated_readme/img/img_2.png" height="250px"/>
1. Haz click en el cuadro 'Text Field' y arrástralo al borde izquierdo de tu View, apróximadamente 1/3 debajo del borde superior
1. Aumenta la longitud del campo de texto arrastrando el lado derecho hasta el borde derecho de tu View
1. Cambia el texto de marcador de posición
    1. En el Utilities Slider, ubicado en la columna derecha de Xcode, encuentra el Attributes Inspector (4to icono en la barra superior del Utilities Slider)
    1. Escribe 'Nueva tarea' en el campo 'Placeholder'
1. Tu storyboard debe verse así: ![](/img/img_3.png)
1. Presiona el botón de ejecutar en la esquina superior izquierda de xCode - ahora debe aparecer una pantalla blanco con un campo de texto que dice 'Nueva tarea' (no te angusties si el campo de texto excede el largo de la pantalla)

## Uniendo nuestras vistas: The storyboard

##### Posicionando el campo de texto utilizando Auto Layout
Cuando corres tu código, puedes cambiar la orientación simplemente con ir a 'Hardware' y seleccionando uno de los botones de rotación. Fíjate que cuando lo haces, tu campo de texto no ajusta su tamaño automáticamente. Vamos a enfocarnos en eso.

1. En el navegador del proyecto en la parte más lejana izquieda de Xcode, selecciona Main.storyboard
1. Selecciona el campo de texto (Text Field) en Vista (View)
1. Establece el espacio de arriba en la parte de arriba
  1. Control+Click y arrastra del Text Field al área justo encima de él, el cual debe de estar sobresaltado en azul y dice 'View'
  1. Suelta lo que arrastraste
  1. Selecciona 'Top Space to Top Layout Guide' que se encuentra en el menú pequeño de color negro.
1. Establece el espacio 'Líder' en la parte izquierda
  1. Control+Click y arrastra del 'Text Field' hacia el área izquierda de la vista, la cual debe de estar resaltada en azul y debe de decir 'View'
  1. Suelta lo que arrastraste
  1. Selecciona 'Leading Space to Container Margin' que se encuentra en el menú pequeño de color negro.
1. Establece el espacio de 'arrastre' en la derecha
  1. Control+Click y arrastra del Text Field al área derecha de la vista, la cual debe de estar resaltada en azul y decir ‘View’
  1. Suelta lo que arrastraste
  1. Selecciona 'Trailing Space to Container Margin' del pequeño menú negro
1. Checkpoint: Corre tu código
  1. Debes de ser capaz de ver el Text Field con el mismo espaciamiento en cada lado y en la parte superior.
  1. En la barra superior de tu computadora, da click en ‘Hardware’ y selecciona ‘Rotate Left’ para entrar en vista horizontal.
  1. El margen superior, izquierdo y derecho deben coincidir con la vista vertical (normal).

##### Crear un table view controller
1. En el navegador del proyecto, que se encuentra en la parte de la izquierda de Xcode, selecciona Main.storyboard
1. En la librería de Objetos, busca el table view controller.
1. Arrastra el table view controller y suéltalo en el lienzo (canvas). Si te falta espacio, da click derecho en el lienzo y haz zoom out.
<Asegurate de haber hecho zoom de 100%>
<view o view controller>
1. Selecciona la flecha en la izquierda de tu controlador de vista
1. Arrástralo hasta tu table view controller para establecer tu table view controller como escena inicial.
1. Tu lienzo debe de parecer algo así: ![](/img/img_4.png)
1. Checkpoint: Corre tu código - debes de ver una tabla vacía

##### Agregar un ‘segue’ para navegar hacia adelante
1. Selecciona tu table view controller 
1. Con el controlador de view seleccionado, escoge Editor > Embed In > Navigation Controller
1. En el lienzo, selecciona el área de título más recientemente en tu table view (o en el esquema de vista selecciona Navigation Item bajo el controlador Table View)
1. ![](/img/img_5.png)
1. En el inspector de atributos, ingresa 'creada My To-Do List' en el área de título (Title field)
1. Agrega un botón de '+'
  1. Arrastra un botón de barra desde la librería de objetos, hasta la derecha de la barra de navegación en el table view controller
  1. Selecciona el botón de barra más reciente.
  1. En el inspector de Atributos, cambia el identificador de un Custom por un Add
1. Checkpoint: Corre tu código - debes de ser capaz de ver tu botón de +, pero no va a hacer nada, aún.

##### Configurar el botón de agregar
1. Control+Click y arrastra del botón de agregar a tu controlador original de vista (View Controller)
1. Suelta lo que arrastraste y selecciona 'present modally'
1. Checkpoint: Corre tu código- Da click en el botón de + y la vista de New Todo debe de aparecer

##### Agregar el navigation controller al view controller
1. Seleccionar el view controller
<no confundir esto con el table list view controller>
1. Con el view controller seleccionado, ir a Editor > Embed In > Navigation Controller
1. En el canvas, seleccionar el área de título recientemente agregado en tu table view (o en el outline view, seleccionar Navigation Item debajo de Table View Controller).
1. En el Attribute Inspector, escribe 'Add Todo' en el campo de título.
1. Agregar el botón 'Done' a la derecha del título
  1. Agrega un Bar Button Item del Object Library a la derecha del navigation bar en el table view controller
  1. Seleccionar el botón que acabas de agregar
  1. En el Attributes inspector, encuentra la opción Identifier en la sección Bar Button Item. Escoge 'Done' del menú que aparece.
1. Agregar el botón de 'Cancel' a la izquierda del título
  1. Agrega un Bar Button Item del Object Library a la izquierda del navigation bar en el table view controller
  1. Seleccionar el botón que acabas de agregar
  1. En el Attributes inspector, encuentra la opción Identifier en la sección Bar Button Item. Escoge ‘Cancel’ del menú que aparece.

1. ![](/img/img_6.png)
1. Checkpoint: Presiona el botón para correr tu aplicación - deberás ver tus nuevos botones 'Done' y 'Cancel' pero aún no harán nada.

## Finalmente, programación: Swift

##### Crea tu propio view controller que sea una subclase de UIViewController
1. Ve a File > New > File (or press Command-N)
1. Llénalo de la siguiente manera ![](/img/img_7.png)
1. Click en Next, y Create.
1. La sección Targets por default tendrá tu app seleccionada y tus tests sin seleccionar. Eso está perfecto, entonces dejémoslo así.
1. Click en Create

Ahora que puedes usar tu propia subclase de view controller, necesitarás que el storyboard sepa que debe usar tu clase en lugar del view controller genérico.

1. En el navegador del proyecto, selecciona Main.storyboard
1. Selecciona tu View Controller (en el Outline View, esto es 'View Controller' debajo de 'Add a todo Scene')
1. En el Identity inspector, abre el menú de Class.
1. Selecciona AddToDoItemViewController

##### Crea tu propio table view controller que sea una subclase de UITableViewController
1. Ve a File > New > File (or press Command-N)
1. En la caja de diálogo, selecciona la Cocoa Touch Class debajo de iOS
1. ![](/img/img_8.png)
1. Click en Next
1. Click en Next, y Create
1. La sección Targets por default tendrá tu app seleccionada y tus tests sin seleccionar. Eso está perfecto, entonces dejémoslo así.
1. En el navegador del proyecto, selecciona Main.storyboard
1. Selecciona tu **Table** View Controller (en el Outline View, esto es 'Table View Controller' debajo de 'Todo list Scene')
1. En el Identity inspector, abre el menú de Class.
1. Selecciona ToDoListTableViewController

##### Conectar los botones Cancel y Done al exit segue

1. Navega al archivo TodoListTableTableViewController.swift
1. Agrega la siguiente función (esto registra la accióny permite que se conecte con el storyboard):
  ```swift
  @IBAction func unwindToList(segue: UIStoryboardSegue) {
      println("Unwinding")
  }

  ```
1. Navega a tu storyboard
1. En el canvas, haz Control-drag del botón 'Cancel' al Exit item de arriba (el objeto de arriba a la derecha de los tres <reword>)
1. Escoge unwindToList: del menu
1. Haz lo mismo para el botón 'Done' 
1. Checkpoint: Corre tu aplicación - cuando navegues a tu botón de ‘Add’, tus botones de ‘Cancel’ y ‘Done’ deben llevarte al Table View. 

##### Crear la clase Data
1. Ve a File > New > File
1. Selecciona Cocoa Touch Class y haz click en Next
1. Llénalo de la siguiente manera ![](/img/img_9.png)
1. Click en Next, y Create
Tu clase debe verse de la siguiente manera
  ```swift
  import UIKit

  class ToDoItem: NSObject {

  }
  ```

##### Llena tu clase TodoItem
1. De la siguiente manera:
  ```swift
  import UIKit

  class TodoItem: NSObject {
    let itemName: String
    var completed: Bool

    init(itemName: String, completed: Bool = false) {
        self.itemName = itemName
        self.completed = completed
    }
  }
  ```

##### Crea en tu table view controller un arreglo de TodoItems
1. Ve a tu archivo TodoTableListViewController.swift
1. Crea un arreglo de la clase TodoItems:
  ```
  var todoItems: [TodoItem] = []

  ```
1. Crea una función loadInitialData que llene el arreglo con tareas básicas de prueba:
  ```swift
  func loadInitialData() {
      todoItems = [
          TodoItem(itemName: "Go to the dentist"),
          TodoItem(itemName: "Fetch groceries"),
          TodoItem(itemName: "Sleep")
      ]
  }

  ```
1. Usa la función que acabas de crear para cargar los datos en el viewDidLoad:
  ```swift
  override func viewDidLoad() {
      super.viewDidLoad()
      loadInitialData()
  }

  ```
1. Haz que tu tabla solamente tenga una sección:
  ```swift
  override func numberOfSectionsInTableView(tableView: UITableView!) -> Int {
      return 1
  }

  ```
1. Enseguida crea una función que regrese el número de filas por sección. Como sólo tenemos una sección, esto retornará la cantidad de todoItems. Agrega la siguiente función:
  ```swift
  override func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
      return todoItems.count
  }

  ```
<this function looks retarded because: https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Functions.html#//apple_ref/doc/uid/TP40014097-CH10-XID_202 (go to External Parameter Names>
1. La última función que tendremos que generar es UITableViewCells para cada renglón
  ```swift
    override func tableView(tableView: UITableView, cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {
      let tempCell = tableView.dequeueReusableCellWithIdentifier("ListPrototypeCell") as UITableViewCell
      let todoItem = todoItems[indexPath.row]

      // Downcast from UILabel? to UILabel
      let cell = tempCell.textLabel as UILabel!
      cell.text = todoItem.itemName

      return tempCell
  }
  ```
1. IEn el proyecto, ve al Main.storyboard
1. En el Todo list TableView selecciona el Prototype Table View Cell
1. En los Utilities a la derecha, ve al Attributes Inspector (4 ícono de izquierda a derecha)
1. Para el Identifier escribe `ListPrototypeCell`
1. Observa: ![](/img/img_10.png)
1. Checkpoint - Corre la aplicación. Deben aparecer las tareas básicas que llenaste como "Go to the dentist", "Fetch groceries", "Sleep"

##### Marcar elemento completado
1.  En el navegador del proyecto selecciona TodoListTableViewController.swift
1. Agrega un  tableView en la función de selección para marcar todoItems como completados
  ```swift
  Sobre escribe la  func tableView(tableView: UITableView, didSelectRowAtIndexPath indexPath: NSIndexPath) {
    tableView.deselectRowAtIndexPath(indexPath, animated: false)

    let tappedItem = todoItems[indexPath.row] as TodoItem
    tappedItem.completed = !tappedItem.completed

    tableView.reloadRowsAtIndexPaths([indexPath], withRowAnimation: UITableViewRowAnimation.None)
  }
  ```
1. Modifica la función de celda de visualización de tableView para tener un checkmark si el elemento ha sido completado

  ```swift
  if (todoItem.completed) {
      tempCell.accessoryType = UITableViewCellAccessoryType.Checkmark;
  } else {
      tempCell.accessoryType = UITableViewCellAccessoryType.None;
  }
  ```
1. La versión final:
  ```swift
  override func tableView(tableView: UITableView, cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {
    let tempCell = tableView.dequeueReusableCellWithIdentifier("ListPrototypeCell") as UITableViewCell
    let todoItem = todoItems[indexPath.row]

    // Downcast from UILabel? to UILabel
    let cell = tempCell.textLabel as UILabel!
    cell.text = todoItem.itemName

    if (todoItem.completed) {
        tempCell.accessoryType = UITableViewCellAccessoryType.Checkmark;
    } else {
        tempCell.accessoryType = UITableViewCellAccessoryType.None;
    }

    return tempCell
  }
  ```
1. Checkpoint - corre la aplicación, selecciona un elemento y un check marck debe de aparecer al lado de él, selecciónalo otra vez para hacer que el check marck desaparezca

##### Por último - agregar nuevos elementos
1. En el navegador del proyecto selecciona Main.storyboard
1. En la vista de esquema, selecciona el objeto AddTodoItemViewController 
1. Da click en el botón de Assistant en la parte superior derecha de la ventana de herramientas, para abrir el asistente de edición (El que parece un pequeño traje)
1. El editor a la derehca debe de aparecer con AddTodoItemViewController.swift desplegado. Si no se despliega, selecciona el nombre del archivo en el editor a la derecha y selecciona AddTodoItemViewController.swift
1. Selecciona el text field en tu storyboard
1. ![](/img/img_11.png)
1. Control + arrastra del text field en tu canvas al código que se despliega en el editor en la derecha, en algún lugar dentro de la clase, y tipo textField como nombre
1. Da click a Connect. Esto debe de agregar el siguiente código: ```@IBOutlet weak var textField: UITextField!```
1. Haz lo mismo para el botón de completado (Done), llamándolo 'doneButton'. En tu código debe de parecer algo como ```@IBOutlet weak var doneButton: UIBarButtonItem!```
1. Siguiente, vamos a darle a nuestro controlador un todoItem que va a guardar la información de nuestro 'add' : ```var todoItem: TodoItem = TodoItem(itemName: "")```
1. Por supuesto, también necesitamos ser capaces de tomar información de la entrada del usuario y asignarla a su variable :

  ```swift
  override func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject!) {
    if (countElements(self.textField.text) > 0) {
        self.todoItem = TodoItem(itemName: self.textField.text)
    }
  }  
  ```
1. Ahora, necesitámos regresar a TodoListTableTableViewController.swift  y agregar un unwind el cual toma información que AddTodoItemViewController.swift contiene y la coloca en el arreglo de todoItems:
  ```swift
  @IBAction func unwindAndAddToList(segue: UIStoryboardSegue) {
    let source = segue.sourceViewController as AddTodoItemViewController
    let todoItem:TodoItem = source.todoItem

    if todoItem.itemName != "" {
        self.todoItems.append(todoItem)
        self.tableView.reloadData()
    }
  }
  ```
1. Por último, selecciona Main.storyboard en el navegador de proyecto
1. En el canvas, Control-arrastra del botón 'Done' hacia el elemento Exit y selecciona unwindAndAddToList
1. Checkpoint: Corre tu app - debes de ser capaz de agregar elementos!

## Eso eso!
Como se había mencionado anteriormente, amámos la retroalimentación - por favor coloca ‘issues’ sobre lo que sea que sientas que falte, o envía un correo al autor directamente jadekler@gmail.com.

  [1]: http://stackoverflow.com/questions/24029586/xcode-6-storyboard-unwind-segue-with-swift-not-connecting-to-exit
