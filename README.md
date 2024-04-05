# Elderly_Medication_App-



import java.util.*;

// Medication class to represent each medication

class Medication {
    private String name;
    private String dosage;
    private String frequency;

    public Medication(String name, String dosage, String frequency) {
        this.name = name;
        this.dosage = dosage;
        this.frequency = frequency;
    }

    // Getters for medication details
    public String getName() {
        return name;
    }

    public String getDosage() {
        return dosage;
    }

    public String getFrequency() {
        return frequency;
    }
}

// MedicationSchedule class to manage medication schedule
class MedicationSchedule {
    private Map<String, List<Medication>> schedule;

    public MedicationSchedule() {
        schedule = new HashMap<>();
    }

    // Add medication to schedule for a specific day
    public void addMedication(String day, Medication medication) {
        if (!schedule.containsKey(day)) {
            schedule.put(day, new ArrayList<>());
        }
        schedule.get(day).add(medication);
    }

    // Get medications for a specific day
    public List<Medication> getMedicationsForDay(String day) {
        return schedule.getOrDefault(day, Collections.emptyList());
    }
}

// ReminderSystem class to handle medication reminders
class ReminderSystem {
    // Send reminder for medications
    public void sendReminder(List<Medication> medications, String time) {
        for (Medication medication : medications) {
            System.out.println("Reminder: Take " + medication.getName() + " (" + medication.getDosage() + ") at " + time);
        }
    }
}

// ElderlyWellnessApp class to integrate all features
class ElderlyWellnessApp {
    private MedicationSchedule medicationSchedule;
    private ReminderSystem reminderSystem;
    private Map<String, String> emergencyContacts;

    public ElderlyWellnessApp() {
        medicationSchedule = new MedicationSchedule();
        reminderSystem = new ReminderSystem();
        emergencyContacts = new HashMap<>();
    }

    // Add medication to schedule
    public void addMedicationToSchedule(String day, Medication medication) {
        medicationSchedule.addMedication(day, medication);
    }

    // Set reminder for medications
    public void setReminder(String day, String time) {
        List<Medication> medications = medicationSchedule.getMedicationsForDay(day);
        reminderSystem.sendReminder(medications, time);
    }

    // Add emergency contact
    public void addEmergencyContact(String name, String phoneNumber) {
        emergencyContacts.put(name, phoneNumber);
    }

    // Get emergency contact information
    public String getEmergencyContact(String name) {
        return emergencyContacts.getOrDefault(name, "Emergency contact not found");
    }
}
 
  class Main {
    public static void main(String[] args) {
        // Creating an instance of ElderlyWellnessApp
        ElderlyWellnessApp app = new ElderlyWellnessApp();

        // Adding medications to the schedule
        app.addMedicationToSchedule("Monday", new Medication("Aspirin", "1 tablet", "Morning"));
        app.addMedicationToSchedule("Monday", new Medication("Vitamin C", "1 tablet", "Evening"));

        // Setting reminder for Monday
        app.setReminder("Monday", "8:00 AM");

        // Adding emergency contacts
        app.addEmergencyContact("Doctor", "6376171236");

        // Getting emergency contact information
        String doctorContact = app.getEmergencyContact("Doctor");
        System.out.println("Doctor's Contact: " + doctorContact);
    }
}
 


