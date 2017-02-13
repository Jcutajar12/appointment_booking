# appointment_booking
//Takes in user appointment, and then can display it back to the user.

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import java.util.LinkedList;
import javax.swing.JOptionPane;
import java.util.Iterator;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;


public class AppointmentBook extends JFrame 
{ 
    JButton addApmtButton = new JButton("Add Appointment");
    JButton removeApmtButton = new JButton("Remove Appointment");
    JButton displayApmtButton = new JButton("Display Appointments");
    LinkedList <String> myList = new LinkedList <String> ();
    String pattern = "MM/dd/YYYY";
   
    public static void main(String args[])
    {

        AppointmentBook demo = new AppointmentBook();
        demo.setSize(400,150);
        demo.setDefaultCloseOperation(EXIT_ON_CLOSE);
        demo.setTitle("Appointment Book");
        demo.createGUI();  
        demo.setVisible(true);
    }
    
    public void createGUI()
    {
        Container window = getContentPane();
        window.setLayout(new FlowLayout());
        addApmtButton.addActionListener(new AddApmtAction());
        window.add(addApmtButton);
        removeApmtButton.addActionListener(new RemoveApmtAction());
        window.add(removeApmtButton);
        displayApmtButton.addActionListener(new DisplayApmtAction());
        window.add(displayApmtButton);
    }
    
    private class AddApmtAction implements ActionListener {
        public void actionPerformed(ActionEvent event){
            String name = JOptionPane.showInputDialog("Enter the name of the appointment");
            String userDate = JOptionPane.showInputDialog("Enter the date of your appointment as MM/DD/YYYY");
            SimpleDateFormat format = new SimpleDateFormat(pattern);
            try {
              Date date = format.parse(userDate);
            }
            catch(ParseException e){
            	 JOptionPane.showMessageDialog(new JFrame(), "That is the Wrong format", "Error", JOptionPane.ERROR_MESSAGE);

            }
          
           
            myList.addFirst(name + " " + userDate);
            //myList.addFirst(JOptionPane.showInputDialog("Enter the name of the appointment"));
        }
    }
    
    private class RemoveApmtAction implements ActionListener {
        public void actionPerformed(ActionEvent event){
            try{
                JOptionPane.showMessageDialog(null,myList.removeFirst() + " was removed", "Remove Item", JOptionPane.INFORMATION_MESSAGE);
            }
            catch (Exception e){
                JOptionPane.showMessageDialog(null, "List empty - nothing removed", "Remove Error", JOptionPane.ERROR_MESSAGE);
            }
        }
    }
    
    private class DisplayApmtAction implements ActionListener {
        public void actionPerformed(ActionEvent event){
            Iterator myIterator = myList.iterator();
            String names = new String("");
            while (myIterator.hasNext()){
                names += " " + myIterator.next();
            }
            JOptionPane.showMessageDialog(null,"Appointments \n" + names, "Message", JOptionPane.INFORMATION_MESSAGE);
        }
    }
}
