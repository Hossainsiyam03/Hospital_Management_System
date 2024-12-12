import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.List;

public class HospitalManagementSystem extends JFrame {

    public HospitalManagementSystem() {
        Receptionist1 receptionist1 = new Receptionist1();
        setTitle("Hospital Management System");
        setSize(600, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(null);

        JButton addPatientButton = new JButton("Add Patient");
        addPatientButton.setBounds(90, 70, 150, 25);
        add(addPatientButton);

        JButton addDoctorButton = new JButton("Add Doctor");
        addDoctorButton.setBounds(90, 120, 150, 25);
        add(addDoctorButton);

        JButton viewPatientsButton = new JButton("View Patients");
        viewPatientsButton.setBounds(310, 70, 150, 25);
        add(viewPatientsButton);

        JButton viewDoctorsButton = new JButton("View Doctors");
        viewDoctorsButton.setBounds(310, 120, 150, 25);
        add(viewDoctorsButton);

        JButton appointmentButton = new JButton("Appointment Schedule");
        appointmentButton.setBounds(90, 170, 200, 25);
        add(appointmentButton);

        JButton viewAppointmentsButton = new JButton("View Appointments");
        viewAppointmentsButton.setBounds(310, 170, 150, 25);
        add(viewAppointmentsButton);

        JButton ExitButton = new JButton("Exit");
        ExitButton.setBounds(170, 300, 200, 25);
        add(ExitButton);

        ExitButton.addActionListener(new ActionListener(){
            public void actionPerformed(ActionEvent e) {
                    dispose();
                    new LoginScreen().setVisible(true);
            }
        }
        );

        addPatientButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String name = JOptionPane.showInputDialog("Enter Patient Name:");
                int age = Integer.parseInt(JOptionPane.showInputDialog("Enter Patient Age:"));
                String problem = JOptionPane.showInputDialog("Enter Patient Problem:");
                String Address = JOptionPane.showInputDialog("Present Address:");
                String Phone = JOptionPane.showInputDialog("Phone Number:");

                receptionist1.addPatient(new Patient(name, age, problem, Address,Phone));
                JOptionPane.showMessageDialog(null, "Patient Added Successfully");
            }
        }
        );

        addDoctorButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String name = JOptionPane.showInputDialog("Enter Doctor Name:");
                String specialization = JOptionPane.showInputDialog("Enter Doctor Specialization:");
                String Phone = JOptionPane.showInputDialog("Phone Number:");
                int Fees = Integer.parseInt(JOptionPane.showInputDialog("Doctor Fees:"));
                String DoctorId = JOptionPane.showInputDialog("DoctorID:");

                receptionist1.addDoctor(new Doctor(name, specialization,Phone,Fees,DoctorId));
                JOptionPane.showMessageDialog(null, "Doctor Added Successfully");
            }
        });

        viewPatientsButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                List<Patient> patients = Receptionist1.getPatients();
                if (patients == null || patients.isEmpty()) {
                    JOptionPane.showMessageDialog(null, "Patient Records are not available.");
                } else {
                    StringBuilder patientsList = new StringBuilder("Patients List:\n");
                    for (Patient patient : Receptionist1.getPatients()) {
                        patientsList.append(patient).append("\n");
                    }
                    JOptionPane.showMessageDialog(null, patientsList.toString());
                }
            }
        }
        );

        viewDoctorsButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                List<Doctor> doctors = Receptionist1.getDoctors();
                if (doctors == null || doctors.isEmpty()) {
                    JOptionPane.showMessageDialog(null, "No doctors are available.");
                }
                else {
                    StringBuilder doctorsList = new StringBuilder("Doctors List:\n");
                    for (Doctor doctor : Receptionist1.getDoctors()) {
                        doctorsList.append(doctor).append("\n");
                    }
                    JOptionPane.showMessageDialog(null, doctorsList.toString());
                }
            }
        }
        );

        appointmentButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                if (Receptionist1.getDoctors().isEmpty() || Receptionist1.getPatients().isEmpty()) {
                    JOptionPane.showMessageDialog(null, "Please add both doctors and patients first.");
                } else {

                    String patientName = JOptionPane.showInputDialog("Enter Patient's Name:");
                    String doctorName = JOptionPane.showInputDialog("Enter Doctor's Name:");
                    String DoctorId = JOptionPane.showInputDialog("Enter Doctor's Name:");
                    String dateTime = JOptionPane.showInputDialog("Enter Appointment Date & Time (yyyy-MM-dd):");

                    Appointment appointment = new Appointment(patientName, doctorName,DoctorId, dateTime);
                    Receptionist1.scheduleAppointment(appointment);
                    JOptionPane.showMessageDialog(null, "Appointment Scheduled Successfully");
                }
            }
        }
        );
        viewAppointmentsButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                if (Receptionist1.getAppointments().isEmpty()) {
                    JOptionPane.showMessageDialog(null, "There are no Appointments Schedule Inserted.");

                } else {
                    StringBuilder appointmentsList = new StringBuilder("Appointments List:\n");
                    for (Appointment appointment : Receptionist1.getAppointments()) {
                        appointmentsList.append(appointment).append("\n");
                    }
                    JOptionPane.showMessageDialog(null, appointmentsList.toString());
                }
            }
        }
        );

        setVisible(true);
    }
}


public class LoginScreen extends JFrame {
    private JTextField usernameField;
    private JPasswordField passwordField;
    private JButton loginButton;

    public LoginScreen() {
        setTitle("ParaDox Hospital");
        setSize(700, 450);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(null);

        JLabel usernameLabel = new JLabel("Username:");
        usernameLabel.setBounds(140, 100, 80, 25);
        add(usernameLabel);

        usernameField = new JTextField();
        usernameField.setBounds(220, 100, 160, 25);
        add(usernameField);

        JLabel passwordLabel = new JLabel("Password:");
        passwordLabel.setBounds(140, 140, 80, 25);
        add(passwordLabel);

        passwordField = new JPasswordField();
        passwordField.setBounds(220, 140, 160, 25);
        add(passwordField);

        loginButton = new JButton("Login");
        loginButton.setBounds(380, 180, 80, 25);
        add(loginButton);


        loginButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());

                if (username.equals("siam1223") && password.equals("siam1223")) {
                    JOptionPane.showMessageDialog(null, "Login Successful");
                    dispose();
                    new HospitalManagementSystem();//main function suru korsi
                }
                else {
                    JOptionPane.showMessageDialog(null, "Invalid Username or Password");
                }
            }
        });
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new LoginScreen().setVisible(true));
    }
}


public class Receptionist1 {
    private static ArrayList<Doctor> doctors = new ArrayList<>();
    private static ArrayList<Patient> patients = new ArrayList<>();
    private static ArrayList<Appointment> appointments = new ArrayList<>();

    public void addDoctor(Doctor doctor) {
        doctors.add(doctor);
    }

    public void addPatient(Patient patient) {
        patients.add(patient);
    }
    public static void scheduleAppointment(Appointment appointment) {
        appointments.add(appointment);
    }

    public static ArrayList<Doctor> getDoctors() {
        return doctors;
    }

    public static ArrayList<Patient> getPatients() {
        return patients;
    }
    public static ArrayList<Appointment> getAppointments() {
        return appointments;
    }
}
public class Patient {
    private  String name;
    private int age;
    private String problem;
    private String Address;
    private String Phone;


    public Patient(String name, int age, String problem, String Address,String Phone) {
        this.name = name;
        this.age = age;
        this.problem = problem;
        this.Address=Address;
        this.Phone=Phone;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public String getProblem() {
        return problem;
    }
    public String getAddress() {
        return Address;
    }
    public String getPhone() {
        return Phone;
    }

    public String toString() {
        return "Patient Name: " + name + "  Age: " + age + "  Problem: " + problem +"  Address: "+ Address+"  Phone: "+Phone;
    }
}

public class Doctor {
    private String name;
    private String specialization;
    private String Phone;
    private int Fees;
    private String DoctorId;

    public Doctor(String name, String specialization,String Phone,int Fees, String DoctorId) {
        this.name = name;
        this.specialization = specialization;
        this.Phone=Phone;
        this.Fees=Fees;
        this.DoctorId=DoctorId;
    }
    public String getName() {
        return name;
    }
    public String getSpecialization() {
        return specialization;
    }
    public String getPhone() {
        return Phone;
    }
    public int getFees() {
        return Fees;
    }
    public String getDoctorId() {
        return DoctorId;
    }

    public String toString() {
        return "Doctor Name: " + name + "Specialization: " + specialization +"Phone Number: "+Phone+"Doctor Fees: "+Fees+"Doctor Id: "+DoctorId;
    }
}

