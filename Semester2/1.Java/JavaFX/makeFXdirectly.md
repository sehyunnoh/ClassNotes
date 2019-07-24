```java

package myfirstjavafx;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.stage.Stage;

public class MyFirstJavaFX extends Application{

    public static void main(String[] args) {
        Application.launch(args);
        
    }

    @Override
    public void start(Stage primaryStage) throws Exception {
        
        primaryStage.setTitle("My first Application");
        
        Label label = new Label("Hello World, JavaFX!");
        Scene scene = new Scene(label, 400, 200);
        primaryStage.setScene(scene);
        
        
        primaryStage.show();
    }
    
}
```