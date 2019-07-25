## result
```console
Line Item Total: 2.99
New Line Item Total: 29.90
New Line Item Total: 20.00
```
**controller**
```java
package bindingexercise2;

import java.net.URL;
import java.util.ResourceBundle;
import javafx.beans.property.DoubleProperty;
import javafx.beans.property.IntegerProperty;
import javafx.beans.property.SimpleDoubleProperty;
import javafx.beans.property.SimpleIntegerProperty;
import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.fxml.Initializable;
import javafx.scene.control.Label;

public class FXMLDocumentController implements Initializable {

    @FXML
    private Label label;

    @FXML
    private void handleButtonAction(ActionEvent event) {
    }

    IntegerProperty quantity = new SimpleIntegerProperty(1);
    DoubleProperty unitPrice = new SimpleDoubleProperty(2.99);
    DoubleProperty lineItemTotal = new SimpleDoubleProperty();

    @Override
    public void initialize(URL url, ResourceBundle rb) {
        
        lineItemTotal.bind(quantity.multiply(unitPrice));

        System.out.printf("Line Item Total: %.2f%n", lineItemTotal.get());
        quantity.set(10);
        System.out.printf("New Line Item Total: %.2f%n", lineItemTotal.get());
        unitPrice.set(2.0);
        System.out.printf("New Line Item Total: %.2f%n", lineItemTotal.get());
    }
}
```
