## result
```console
5.0
DoubleProperty [bean: Radius: 5.0, name: radius, value: 5.0]
```

**Circle.java**
```java
package bindingexercise4;

import javafx.beans.property.DoubleProperty;
import javafx.beans.property.SimpleDoubleProperty;

public class Circle {

    private final DoubleProperty radius = new SimpleDoubleProperty(this, "radius");

    public Circle() {
    }

    public final void setRadius(double radius) {
        if (radius >= 0) {
            this.radius.set(radius);
        } else {
            throw new IllegalArgumentException("Error: radius must be 0 or more.");
        }
    }

    public final double getRadius() {
        return radius.get();
    }

    public final DoubleProperty radiusProperty() {
        return radius;
    }

    @Override
    public String toString() {
        return String.format("Radius: %.1f", radius.get());
    }

}
```

**controller**
```java
package bindingexercise4;

import java.net.URL;
import java.util.ResourceBundle;
import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.fxml.Initializable;
import javafx.scene.control.Label;

public class FXMLDocumentController implements Initializable {
    
    @FXML
    private Label label;
    
    @FXML
    private void handleButtonAction(ActionEvent event) {
        System.out.println("You clicked me!");
        label.setText("Hello World!");
    }
    
    @Override
    public void initialize(URL url, ResourceBundle rb) {
        Circle circle = new Circle();
        circle.setRadius(5.0);
        System.out.println(circle.getRadius());
        System.out.println(circle.radiusProperty());
    }    
    
}
```