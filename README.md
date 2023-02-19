# Event-Driven-Programming-and-Animations
a program that enables the user to drag the vertices of a triangle and displays the angles dynamically as the triangle shape changes

import java.text.DecimalFormat;
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.layout.Pane;
import javafx.scene.shape.Circle;
import javafx.scene.shape.Line;
import javafx.scene.text.Text;
import javafx.stage.Stage;

/**
 *
 * @author OnthaitleMash
 */
public class DisplayAngles extends Application
{
    @Override
    public void start(Stage primaryStage)
    {
        DecimalFormat formatter = new DecimalFormat("###.00");
        Pane pane = new Pane();
    
        Circle circle = new Circle();
        circle.setRadius(5);
        circle.setCenterX(25);
        circle.setCenterY(50);
        
        Circle circle1 = new Circle();
        circle1.setRadius(5);
        circle1.setCenterX(75);
        circle1.setCenterY(150);
        
        Circle circle2 = new Circle();
        circle2.setRadius(5);
        circle2.setCenterX(125);
        circle2.setCenterY(250);

        Line line = new Line();
        Line line1 = new Line();
        Line line2 = new Line();
        
        Text text = new Text();
        Text text1 = new Text();
        Text text2 = new Text();
        
        ComputeAngles angles = new ComputeAngles(
                circle.getCenterX(), circle.getCenterY(),
                circle1.getCenterX(), circle1.getCenterY(),
                circle2.getCenterX(), circle2.getCenterY());
        
        angles.calulateSides();
        
        text.setText(String.valueOf(angles.calculateAngleA()));
        text1.setText(String.valueOf(angles.calculateAngleB()));
        text2.setText(String.valueOf(angles.calculateAngleC()));
        System.out.println(angles.getX3());
        
        text.xProperty().bind(circle.centerXProperty().add(10));
        text.yProperty().bind(circle.centerYProperty());
        
        text1.xProperty().bind(circle1.centerXProperty().add(10));
        text1.yProperty().bind(circle1.centerYProperty());
        
        text2.xProperty().bind(circle2.centerXProperty().add(10));
        text2.yProperty().bind(circle2.centerYProperty());
        
        circle.setOnMouseDragged(e ->
        {
           angles.setX1(e.getX());
           angles.setY1(e.getY());
           angles.calulateSides();
           
           circle.setCenterX(e.getX());
           circle.setCenterY(e.getY());
           
           line.startXProperty().bind(circle.centerXProperty());
           line.startYProperty().bind(circle.centerYProperty());
           line1.endXProperty().bind(circle.centerXProperty());
           line1.endYProperty().bind(circle.centerYProperty());
           
           text.setText(String.valueOf(formatter.format(angles.calculateAngleA())));
           text1.setText(String.valueOf(formatter.format(angles.calculateAngleB())));
           text2.setText(String.valueOf(formatter.format(angles.calculateAngleC())));
        });
       
        circle1.setOnMouseDragged(e ->
        {
            
           angles.setX2(e.getX());
           angles.setY2(e.getY());
           angles.calulateSides();
           
           circle1.setCenterX(e.getX());
           circle1.setCenterY(e.getY());
           
           line1.startXProperty().bind(circle1.centerXProperty());
           line1.startYProperty().bind(circle1.centerYProperty());
           line2.endXProperty().bind(circle1.centerXProperty());
           line2.endYProperty().bind(circle1.centerYProperty());
           
           text.setText(String.valueOf(formatter.format(angles.calculateAngleA())));
           text1.setText(String.valueOf(formatter.format(angles.calculateAngleB())));
           text2.setText(String.valueOf(formatter.format(angles.calculateAngleC())));
        });
       
        circle2.setOnMouseDragged(e ->
        {
            
           angles.setX3(e.getX());
           angles.setY3(e.getY());
           angles.calulateSides();
           
           circle2.setCenterX(e.getX());
           circle2.setCenterY(e.getY());
           
           line2.startXProperty().bind(circle2.centerXProperty());
           line2.startYProperty().bind(circle2.centerYProperty());
           line.endXProperty().bind(circle2.centerXProperty());
           line.endYProperty().bind(circle2.centerYProperty());
           
           text.setText(String.valueOf(formatter.format(angles.calculateAngleA())));
           text1.setText(String.valueOf(formatter.format(angles.calculateAngleB())));
           text2.setText(String.valueOf(formatter.format(angles.calculateAngleC())));
        });
        
        pane.getChildren().addAll(circle, circle1, circle2,
                line, line1, line2,
                text, text1, text2);
        
       
       Scene scene = new Scene(pane);
       primaryStage.setTitle("Exercise15 _20");
       primaryStage.setScene(scene);
       primaryStage.show();
       
    }
    
    public static void main(String[] args) 
    {
        launch();
    }
}

class ComputeAngles 
{
    private double x1;
    private double y1;
    private double x2;
    private double y2;
    private double x3;
    private double y3;
        
    private double a;
    private double b;
    private double c;

    public ComputeAngles() 
    {
    }

    public ComputeAngles(double x1, double y1, double x2, double y2, double x3, double y3) 
    {
        this.x1 = x1;
        this.y1 = y1;
        this.x2 = x2;
        this.y2 = y2;
        this.x3 = x3;
        this.y3 = y3;
    }
    /*
    public ComputeAngles(double x1, double y1) 
    {
        this.x1 = x1;
        this.y1 = y1;
    }
        
    public  ComputeAngles(double x2, double y2) 
    {
        this.x2 = x2;
        this.y2 = y2;
    }
    public ComputeAngles(double x3, double y3) 
    {
        this.x3 = x3;
        this.y3 = y3;
    }
*/
    public ComputeAngles(double x1, double y1, double x2, double y2, double x3, double y3, double a, double b, double c) 
    {
        this.x1 = x1;
        this.y1 = y1;
        this.x2 = x2;
        this.y2 = y2;
        this.x3 = x3;
        this.y3 = y3;
        this.a = a;
        this.b = b;
        this.c = c;
    }

    public void setX1(double x1) 
    {
        this.x1 = x1;
    }

    public void setY1(double y1) 
    {
        this.y1 = y1;
    }

    public void setX2(double x2) 
    {
        this.x2 = x2;
    }

    public void setY2(double y2) 
    {
        this.y2 = y2;
    }

    public void setX3(double x3) 
    {
        this.x3 = x3;
    }

    public void setY3(double y3) 
    {
        this.y3 = y3;
    }

    public void setA(double a) 
    {
        this.a = a;
    }

    public void setB(double b) 
    {
        this.b = b;
    }

    public void setC(double c) 
    {
        this.c = c;
    }
    
    public double getX1() 
    {
        return x1;
    }

    public double getY1() 
    {
        return y1;
    }

    public double getX2() 
    {
        return x2;
    }

    public double getY2() 
    {
        return y2;
    }

    public double getX3() 
    {
        return x3;
    }

    public double getY3() 
    {
        return y3;
    }

    public double geta() 
    {
        return a;
    }

    public double getb() 
    {
        return b;
    }

    public double getc() 
    {
        return c;
    }

    public void calulateSides()
    {
        // Compute three sides
        a = Math.sqrt((x2 - x3) * (x2 - x3) + (y2 - y3) * (y2 - y3));
        b = Math.sqrt((x1 - x3) * (x1 - x3) + (y1 - y3) * (y1 - y3));
        c = Math.sqrt((x1 - x2) * (x1 - x2)+ (y1 - y2) * (y1 - y2));
    }
    
    public double calculateAngleA()
    {
        double A = Math.toDegrees(Math.acos((a * a - b * b - c * c) / (-2 * b * c)));
        
        return A;
    }
    
    public double calculateAngleB()
    {
        double B = Math.toDegrees(Math.acos((b * b - a * a - c * c) / (-2 * a * c)));
        
        return B;
    }
        
    public double calculateAngleC()
    {
        double C = Math.toDegrees(Math.acos((c * c - b * b - a * a) / (-2 * a * b)));
        
        return C;
    }
    
}
