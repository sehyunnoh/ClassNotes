## result
```console
Interest Earned: $50.00
```

**Account.java**
```java
package bindingexercise3;

import javafx.beans.property.DoubleProperty;
import javafx.beans.property.SimpleDoubleProperty;

public class Account {

    private String id = "c-100";
    private final DoubleProperty balance = new SimpleDoubleProperty(this, "balance");
    private final DoubleProperty interestRate = new SimpleDoubleProperty(this, "interestRate", 2.3);

    public Account() {
    }

    public void setId(String id) {
        if (id != null && !id.trim().isEmpty()) {
            this.id = id;
        } else {
            throw new IllegalArgumentException("Error - ID can't be empty.");
        }
    }

    public String getId() {
        return id;
    }

    public final void setBalance(double balance) {
        if (balance >= 0) {
            this.balance.set(balance);
        } else {
            throw new IllegalArgumentException("Error: balance must be 0 or more.");
        }
    }

    public final double getBalance() {
        return balance.get();
    }

    public final void setInterestRate(double rate) {
        if (rate >= 0) {
            interestRate.set(rate);
        } else {
            throw new IllegalArgumentException("Error: interest rate must be greater than 0.");
        }
    }

    public final double getInterestRate() {
        return interestRate.get();
    }

    public final DoubleProperty balanceProperty() {
        return balance;
    }

    public final DoubleProperty interestRateProperty() {
        return interestRate;
    }

    @Override
    public String toString() {
        return String.format("%s Balance: $%.2f", id, balance.get());
    }

}
```

**controller**
```java
package bindingexercise3;

import java.net.URL;
import java.util.ResourceBundle;
import javafx.beans.InvalidationListener;
import javafx.beans.Observable;
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
        Account acct = new Account();
        acct.setBalance(1000.0);
        acct.interestRateProperty().addListener(new InvalidationListener() {
            @Override
            public void invalidated(Observable observable) {
                double totalInterest = acct.getInterestRate() / 100 * acct.getBalance();
                System.out.printf("Interest Earned: $%.2f%n", totalInterest);
            }
        });
        acct.setInterestRate(5.0);

    }

}
```