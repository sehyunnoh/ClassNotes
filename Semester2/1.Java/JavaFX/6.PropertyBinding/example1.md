## result 
```console
Old X Value: 10
x has changed to: 1
New X Value: 1
```
**controller**
```java
package bindingexercise1;

import java.net.URL;
import java.util.ResourceBundle;
import javafx.beans.InvalidationListener;
import javafx.beans.property.IntegerProperty;
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

    @Override
    public void initialize(URL url, ResourceBundle rb) {
        IntegerProperty xValue = new SimpleIntegerProperty(10);
        xValue.addListener(new InvalidationListener() {
            @Override
            public void invalidated(javafx.beans.Observable observable) {
                System.out.println("x has changed to: " + xValue.get());
            }
        });
        System.out.println("Old X Value: " + xValue.get());
        xValue.set(1);
        System.out.println("New X Value: " + xValue.get());
    }
}
```

