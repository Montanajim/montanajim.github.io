Of course, Jim. Below is a **professional, well-structured Java program** that demonstrates the major **layout managers** in **Swing**. I have included examples for:

- **FlowLayout**
- **BorderLayout**
- **GridLayout**
- **BoxLayout**
- **GridBagLayout**

Each layout will be demonstrated in a **tabbed pane**, so you can easily switch between layouts during the demonstration.

Here is the complete code:

```java
/*
Demo of Layout Managers
 */
package j2_layoutmanager_demo;



import javax.swing.*;
import java.awt.*;

class LayoutManagerDemo extends JFrame {

    public LayoutManagerDemo() {
        setTitle("Layout Manager Demonstration");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(600, 400);
        setLocationRelativeTo(null); // Center on screen

        JTabbedPane tabbedPane = new JTabbedPane();

        tabbedPane.addTab("FlowLayout", createFlowLayoutPanel());
        tabbedPane.addTab("BorderLayout", createBorderLayoutPanel());
        tabbedPane.addTab("GridLayout", createGridLayoutPanel());
        tabbedPane.addTab("BoxLayout", createBoxLayoutPanel());
        tabbedPane.addTab("GridBagLayout", createGridBagLayoutPanel());

        add(tabbedPane);

        setVisible(true);
    }

    private JPanel createFlowLayoutPanel() {
        JPanel panel = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 10));
        for (int i = 1; i <= 5; i++) {
            panel.add(new JButton("Button " + i));
        }
        return panel;
    }

    private JPanel createBorderLayoutPanel() {
        JPanel panel = new JPanel(new BorderLayout(5, 5));
        panel.add(new JButton("North"), BorderLayout.NORTH);
        panel.add(new JButton("South"), BorderLayout.SOUTH);
        panel.add(new JButton("East"), BorderLayout.EAST);
        panel.add(new JButton("West"), BorderLayout.WEST);
        panel.add(new JButton("Center"), BorderLayout.CENTER);
        return panel;
    }

    private JPanel createGridLayoutPanel() {
        JPanel panel = new JPanel(new GridLayout(2, 3, 5, 5));
        for (int i = 1; i <= 6; i++) {
            panel.add(new JButton("Button " + i));
        }
        return panel;
    }

    private JPanel createBoxLayoutPanel() {
        JPanel panel = new JPanel();
        panel.setLayout(new BoxLayout(panel, BoxLayout.Y_AXIS));
        for (int i = 1; i <= 5; i++) {
            panel.add(Box.createRigidArea(new Dimension(1, 10))); // Add space between buttons
            panel.add(new JButton("Button " + i));
        }
        return panel;
    }

    private JPanel createGridBagLayoutPanel() {
        JPanel panel = new JPanel(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(5, 5, 5, 5); // Padding around components

        for (int i = 0; i < 3; i++) {
            gbc.gridx = i;
            gbc.gridy = 0;
            panel.add(new JButton("Button " + (i + 1)), gbc);
        }

        gbc.gridx = 0;
        gbc.gridy = 1;
        gbc.gridwidth = 3; // Span across 3 columns
        panel.add(new JButton("Wide Button"), gbc);

        return panel;
    }

//    public static void main(String[] args) {
//        SwingUtilities.invokeLater(LayoutManagerDemo::new);
//    }
}



/**
 *
 * @author jgoudy
 */
public class J2_LayoutManager_Demo {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args)
    {
        
        LayoutManagerDemo LMD = new LayoutManagerDemo();
        
    }
    
}

```

------

### Notes:

- **FlowLayout**: Places components in a line, wrapping as needed.
- **BorderLayout**: Divides the container into five regions (North, South, East, West, Center).
- **GridLayout**: Arranges components in a grid of equal-sized cells.
- **BoxLayout**: Aligns components either vertically (Y_AXIS) or horizontally (X_AXIS).
- **GridBagLayout**: Flexible, allows fine-tuned positioning and sizing.

### References:

- Oracle, *Creating a GUI with Swing - Layout Management* ([link](https://docs.oracle.com/javase/tutorial/uiswing/layout/index.html))
- Oracle, *How to Use BorderLayout* ([link](https://docs.oracle.com/javase/tutorial/uiswing/layout/border.html))
- Oracle, *How to Use BoxLayout* ([link](https://docs.oracle.com/javase/tutorial/uiswing/layout/box.html))
- Oracle, *How to Use GridBagLayout* ([link](https://docs.oracle.com/javase/tutorial/uiswing/layout/gridbag.html))

------

Would you also like me to prepare a simple *screenshot* or a *diagram* showing how each layout looks visually? It could be useful for your classroom if you’re teaching this!