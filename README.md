package com.company;

import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

public class Main
{

    public static void main(String[] args)
    {

        //PersonWriter.write(PersonReader.read(2), "tester2.txt");
        GUI g = new GUI(5, "PUM PUM PUPUPUPUM");
    }
}

class Person
{
    String name;
    String second_name;
    String age;

    public Person(String name1, String second_name1, String age1)
    {
        name = name1;
        second_name = second_name1;
        age = age1;
    }

    public String print()
    {
        String result = "[NAME: " + name + "; SECOND_NAME: " + second_name + "; AGE: " + age + "]\n";
        return result;
    }
}

class PersonWriter
{
    public static void write(Person[] persons, String file)
    {
        try(FileWriter writer = new FileWriter(file, false))
        {
            for(int i = 0; i < persons.length; i++)
            {
                String text = persons[i].print();
                writer.write(text);
            }
            writer.flush();
        }
        catch(IOException ex)
        {

            System.out.println(ex.getMessage());
        }
    }
}

class PersonReader
{
    public static Person[] read(int i)
    {
        Person[] persons = new Person[i];
        for(int j = 0; j < i; j++)
        {
            System.out.println("ENTER DATA OF PERSON " + j);
            Scanner input = new Scanner(System.in);
            String name = input.next();
            String second_name = input.next();
            String age = input.next();
            persons[j] = new Person(name, second_name, age);
        }
        return persons;
    }
}





































package com.company;

import javax.swing.*;
import java.awt.*;

public class GUI extends JFrame
{
    int index = 0;
    public Person[] persons;
    public JTextField name = new JTextField("NAME");
    public JTextField second_name = new JTextField("SECOND_NAME");
    public JTextField age = new JTextField("AGE");
    public JButton add = new JButton("ADD");
    public JButton save = new JButton("SAVE");
    public GUI(int n, String file)
    {
        persons = new Person[n];
        this.setLayout(new FlowLayout());
        this.setSize(500, 100);
        this.setVisible(true);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

        add.addActionListener(e ->
        {
            if(index < n)
            {
                persons[index] = new Person(name.getText(), second_name.getText(), age.getText());
                index++;
                name.setText("");
                second_name.setText("");
                age.setText("");
            }
        });
        save.addActionListener(e ->
        {
            PersonWriter.write(persons, file);
        });

        add(name);
        add(second_name);
        add(age);
        add(add);
        add(save);
    }
}
