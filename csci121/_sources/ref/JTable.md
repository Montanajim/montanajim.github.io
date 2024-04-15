# JTable Component

```java
/*
 *
 * https://docs.oracle.com/javase/tutorial/uiswing/components/table.html#simple
 * https://www.javatpoint.com/java-jtable
 * https://www.javatpoint.com/java-jtable
 *
 *
 * //create table model with data
 * DefaultTableModel model = new DefaultTableModel(data, columns) {
 * @Override
 * public boolean isCellEditable(int row, int column)
 * {
 * return false;
 * }
 * @Override
 * public Class<?> getColumnClass(int columnIndex)
 * {
 * return columnClass[columnIndex];
 * }
 * };
 *
 * // https://codejava.net/java-se/swing/a-simple-jtable-example-for-display
 *
 *
 *
 */
package j2_jtable_lecture;

import java.awt.Component;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.DecimalFormat;
import java.util.ArrayList;
import java.util.Random;
import javax.swing.DefaultCellEditor;
import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.JTextField;
import javax.swing.ListSelectionModel;
import javax.swing.event.ListSelectionListener;
import javax.swing.event.TableModelEvent;
import javax.swing.event.TableModelListener;
import javax.swing.table.DefaultTableModel;
import javax.swing.table.TableColumn;
import javax.swing.table.DefaultTableCellRenderer;
import java.text.NumberFormat;
import javax.swing.RowFilter;
import javax.swing.table.TableModel;
import javax.swing.table.TableRowSorter;

class NumberTableCellRenderer extends DefaultTableCellRenderer {

    public NumberTableCellRenderer() {
        setHorizontalAlignment(JLabel.RIGHT);
    }

    @Override
    public Component getTableCellRendererComponent(JTable table, Object value,
            boolean isSelected, boolean hasFocus, int row, int column) {
        if (value instanceof Number) {
            value = NumberFormat.getNumberInstance().format(value);
        }
        if (value instanceof String) {
            int ivalue = Integer.parseInt(String.valueOf(value));
            value = "$" + NumberFormat.getNumberInstance().format(ivalue);
        }
        return super.getTableCellRendererComponent(table, value, isSelected,
                hasFocus, row, column);
    }

}

/**
 *
 *
 */
public class Frame1 extends javax.swing.JFrame {

    Random RNG;

    int Rows = 15;
    int Cols = 4;
    String[][] mySampleData;
    DefaultTableModel model;

    JTable myTable;
//    ListSelectionListener mySelect;
//    TableModelListener aa;
    ArrayList<JTextField> ALinputFields = new ArrayList();

    String[] myColNames
            = {
                "First Name", "Last Name", "City", "Salary"
            };

    String[] City_Array
            = {
                "Kalispell", "Polson", "Whitefish", "Missoula", "Helena"
            };

    public Frame1() {
        initComponents();

        this.setSize(700, 750);
        this.setLocationRelativeTo(null);

        CreateSampleData();

        //setup data model
        setupDataModel();

        // table setup 
        SetUpMyTable();

        // add the delete button
        addDeleteButton();

        // add the add record
        setupAddRecord();

    }

    private void setupDataModel() {
        final Class[] columnClass = new Class[]{
            String.class, String.class, String.class, Integer.class
        };

        //Setup the data model
        model = new DefaultTableModel(mySampleData, myColNames) {
            @Override
            public boolean isCellEditable(int row, int column) {
                return true;
            }

            @Override
            public Class<?> getColumnClass(int columnIndex) {
                return columnClass[columnIndex];
            }
        };

        myTable = new JTable(model);

    }

    private void SetUpMyTable() {

        // resize the columns automatically
        myTable.setAutoResizeMode(JTable.AUTO_RESIZE_ALL_COLUMNS);

        // set sorting by clicking column header
        myTable.setAutoCreateRowSorter(true);
        myTable.setVisible(true);
        myTable.setEnabled(true);

        // Selection Options
        // ListSelectionModel.MULTIPLE_INTERVAL_SELECTION, 
        // ListSelectionModel.SINGLE_INTERVAL_SELECTION
        // ListSelectionModel.SINGLE_SELECTION
        myTable.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);

        // Make the table editable
        myTable.getModel().addTableModelListener(new TableModelListener() {
            @Override
            public void tableChanged(TableModelEvent e) {
                // for testing 
                printArray();
            }

        });

        SetupCityDropDown();

        formatSalary();

        JScrollPane myScrollPane = new JScrollPane(myTable);
        myScrollPane.setLocation(50, 100);
        myScrollPane.setVisible(true);
        myScrollPane.setSize(600, 400);
        this.add(myScrollPane);

    }

    private void addDeleteButton() {

        int bwith = 72;
        int bheight = 22;

        JButton jbttnDelete = new JButton();

        jbttnDelete.setText("Delete");
        jbttnDelete.setVisible(true);
        jbttnDelete.setSize(bwith, bheight);

        jbttnDelete.setLocation(50, 75);

        jbttnDelete.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                try {
                    int seldelete = myTable.getSelectedRow();
                    if (myTable.getSelectedRow() > -1) {
                        model.removeRow(myTable.getSelectedRow());

                    }
                } catch (Exception ee) {
                    JOptionPane.showMessageDialog(null, ee.getMessage());

                }

                myTable.repaint();

            }
        });

        this.add(jbttnDelete);

    }

    private void setupAddRecord() {

        // Label variables
        int xl = 50, yl = 10, wl = 100, hl = 30, spacel = 10;

        // Textfield variables
        int x = 50, y = 40, w = 100, h = 30, space = 10;

        String[] inLabels
                = {
                    "First Name", "Last Name", "City", "Salary"
                };

        //
        for (int i = 0; i < inLabels.length; i++) {

            var tfLabel = new JLabel();
            tfLabel.setSize(wl, hl);
            tfLabel.setText(inLabels[i]);
            tfLabel.setVisible(true);
            tfLabel.setLocation(xl, yl);

            var tfInput = new JTextField();
            tfInput.setSize(w, h);
            tfInput.setText(inLabels[i]);
            tfInput.setVisible(true);
            tfInput.setText("");
            tfInput.setLocation(x, y);

            ALinputFields.add(tfInput);
            this.add(tfInput);
            this.add(tfLabel);

            x = x + w + space;
            xl = xl + wl + spacel;
        }

        var tfAdd = new JButton();
        tfAdd.setSize(w, h);
        tfAdd.setText("Add");
        tfAdd.setVisible(true);
        tfAdd.setLocation(x, y);

        tfAdd.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                addData();
            }

            private void addData() {
                Object[] newData = new Object[ALinputFields.size()];

                for (int i = 0; i < ALinputFields.size(); i++) {
                    newData[i] = ALinputFields.get(i).getText();
                }

                model.addRow(newData);
            }
        });

        this.add(tfAdd);

    }

    private void SetupCityDropDown() {

        TableColumn cityColumn = myTable.getColumnModel().getColumn(2);
        JComboBox cityCombo = new JComboBox();

        for (int i = 0; i < City_Array.length; i++) {
            cityCombo.addItem(City_Array[i]);
        }

        cityColumn.setCellEditor(new DefaultCellEditor(cityCombo));

    }

    private void formatSalary() {
        DecimalFormat df = new DecimalFormat("###,###,###");
        df.format(111222333);
        myTable.getColumnModel().getColumn(3).setCellRenderer(new NumberTableCellRenderer());

    }

    private void CreateSampleData() {

        String FN, LN, City;
        RNG = new Random();

        String[] FN_Array
                = {
                    "Bob", "Jim", "Jane", "Jody", "Jill", "Tom", "Steve"
                };
        String[] LN_Array
                = {
                    "Rogers", "Smith", "Rodes",
                    "Brady", "Gravey", "Knucles", "Heavers"
                };

        int Salary = 0;

        mySampleData = new String[Rows][Cols];

        for (int r = 0; r < Rows; r++) {

            FN = FN_Array[RNG.nextInt(FN_Array.length)];
            LN = LN_Array[RNG.nextInt(LN_Array.length)];
            City = City_Array[RNG.nextInt(City_Array.length)];
            Salary = RNG.nextInt(500000) + 40000;

            mySampleData[r][0] = FN;
            mySampleData[r][1] = LN;
            mySampleData[r][2] = City;
            mySampleData[r][3] = String.valueOf(Salary);

        }

    }

    /**
     *
     */
    private void printArray() {
        System.out.println("made it to pa");
        for (int r = 0; r < model.getRowCount(); r++) {
            for (int c = 0; c < model.getColumnCount(); c++) {
                //System.out.print(theArray[r][c] + " ");
                System.out.print(model.getValueAt(r, c) + " ");
            }
            System.out.println("");

        }

        System.out.println("\n---------------\n");

    }

    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jButton1 = new javax.swing.JButton();
        jButton2 = new javax.swing.JButton();
        jMenuBar1 = new javax.swing.JMenuBar();
        jMenu1 = new javax.swing.JMenu();
        jmnuPrint = new javax.swing.JMenuItem();
        jmuQuit = new javax.swing.JMenuItem();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        jButton1.setText("jButton1");
        jButton1.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jButton1ActionPerformed(evt);
            }
        });

        jButton2.setText("jButton2");
        jButton2.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jButton2ActionPerformed(evt);
            }
        });

        jMenu1.setText("File");

        jmnuPrint.setAccelerator(javax.swing.KeyStroke.getKeyStroke(java.awt.event.KeyEvent.VK_P, java.awt.event.InputEvent.CTRL_DOWN_MASK));
        jmnuPrint.setText("Print");
        jmnuPrint.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jmnuPrintActionPerformed(evt);
            }
        });
        jMenu1.add(jmnuPrint);

        jmuQuit.setAccelerator(javax.swing.KeyStroke.getKeyStroke(java.awt.event.KeyEvent.VK_Q, java.awt.event.InputEvent.CTRL_DOWN_MASK));
        jmuQuit.setText("Quit");
        jmuQuit.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jmuQuitActionPerformed(evt);
            }
        });
        jMenu1.add(jmuQuit);

        jMenuBar1.add(jMenu1);

        setJMenuBar(jMenuBar1);

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                .addContainerGap(356, Short.MAX_VALUE)
                .addComponent(jButton1)
                .addGap(18, 18, 18)
                .addComponent(jButton2)
                .addGap(41, 41, 41))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addContainerGap()
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(jButton1)
                    .addComponent(jButton2))
                .addContainerGap(507, Short.MAX_VALUE))
        );

        pack();
    }// </editor-fold>                        

    private void jmnuPrintActionPerformed(java.awt.event.ActionEvent evt)                                          
    {                                              

        JFrame myFrame = new JFrame("Message Examples");

        myFrame.setAlwaysOnTop(true);

        try {
            if (!myTable.print()) {
                System.err.println("User Cancellent Printing");

                JOptionPane.showMessageDialog(myFrame,
                        "User Cancellent Printing",
                        "User Cancelled Printing",
                        JOptionPane.ERROR_MESSAGE);

            }
        } catch (java.awt.print.PrinterException ex) {
            JOptionPane.showMessageDialog(myFrame,
                    ex.getMessage(),
                    "Printer Error",
                    JOptionPane.ERROR_MESSAGE);

        }

    }                                         

    private void jmuQuitActionPerformed(java.awt.event.ActionEvent evt)                                        
    {                                            
        System.exit(0);
    }                                       

    private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         
        
      
        String filterText = "Rogers";
        
        
        RowFilter<DefaultTableModel, Object> myRowFilter = RowFilter.regexFilter(filterText, 1);
        TableRowSorter<TableModel> sorter = (TableRowSorter) myTable.getRowSorter();
        
        sorter.setRowFilter(RowFilter.regexFilter(filterText, 1));

    }                                        

    private void jButton2ActionPerformed(java.awt.event.ActionEvent evt) {                                         
        TableRowSorter<TableModel> sorter = (TableRowSorter) myTable.getRowSorter();
        sorter.setRowFilter(RowFilter.regexFilter("", 1));
    }                                        

    /**
     * @param args the command line arguments
     */
    public static void main(String args[]) {
        /*
         * Set the Nimbus look and feel
         */
        //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
        /*
         * If Nimbus (introduced in Java SE 6) is not available, stay with the
         * default look and feel.
         * For details see
         * http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html
         */
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(Frame1.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(Frame1.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(Frame1.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(Frame1.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>
        //</editor-fold>
        //</editor-fold>
        //</editor-fold>

        /*
         * Create and display the form
         */
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new Frame1().setVisible(true);
            }
        });
    }


    // Variables declaration - do not modify                     
    private javax.swing.JButton jButton1;
    private javax.swing.JButton jButton2;
    private javax.swing.JMenu jMenu1;
    private javax.swing.JMenuBar jMenuBar1;
    private javax.swing.JMenuItem jmnuPrint;
    private javax.swing.JMenuItem jmuQuit;
    // End of variables declaration                   
}

```

