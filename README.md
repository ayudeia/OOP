import java.util.Scanner;

class Candidate {
    String name;
    String gender;
    String address;
    int age;
    String initial;


    Candidate(String name, String gender, String address, int age, String initial){
        this.name = name;
        this.gender = gender;
        this.address = address;
        this.age = age;
        this.initial = initial;
    }
}

public class OOP {
    static int idx = 0;
    static Candidate[] candidates = new Candidate[100];
    
    public static void removeCandidate(int candidateNumber) {
        if (candidateNumber >=1 && candidateNumber <=idx) {
            if (candidates[candidateNumber-1] != null) {

            for (int i=candidateNumber-1; i<idx; i++) {
                candidates[i] = candidates[i+1];
            }
            candidates[idx-1] = null;
            idx--;

            displayCandidates();
            } else {
                System.out.println("Invalid candidate number!");
            }   
        
            } else if (candidateNumber == 0) {
                System.out.println("Deletion Canceled!");
            } else {
                System.out.println("Invalid candidate number!");
            }
    }

    public static void displayCandidates() {
        if (idx==0) {
            System.out.println("\nNo Data\n");
        } else {
            System.out.println();
            bubbleSort(candidates, idx);
            for (int i=0; i<idx; i++) {
                 System.out.println(i+1 + " | " + candidates[i].name + " | " + candidates[i].initial + " | " + candidates[i].gender + " | "+ candidates[i].age + " | " + candidates[i].address + " | ");
             }
         }
     }

    public static void main(String[] args){
        int choose = 0;
        boolean inputOk = true;
        Scanner oop = new Scanner(System.in);

        do {
            System.out.println("\n          Power Recruitment");
            System.out.println("          -----------------\n");
            System.out.println("1. Input New Candidate");
            System.out.println("2. View Candidate's Data");
            System.out.println("3. Remove Candidate");
            System.out.println("4.Exit");
        
            try {
                System.out.print("Choose: ");
                choose = oop.nextInt();
                
            } catch (Exception e) {
                System.out.println("Input must be an Integer");
                choose = 0;
                inputOk = false;
            }
            oop.nextLine();

            switch (choose) {
                case 1:
                    String name;
                    String address = "";
                    String gender = "";
                    String[] words;
                    int age;

                    do {
                        System.out.print("Input Candidate's Name [5...20]: ");
                        name = oop.nextLine();
                        words = name.split(" ", 10);
                        if (name.length() < 5 || name.length() > 20) {
                            System.out.println("Name must be 5 and 20 characters!");
                        } else if (words.length < 2) {
                            System.out.println("Name must be at least 2 words!");
                        }
                    } while (name.length() < 5 || name.length() > 20 || words.length < 2);

                    
                    
                    String initial = "";
                    for(int i=0; i<words.length; i++) {
                        initial = initial + words[i].charAt(0);
                    }
                    initial = initial.toUpperCase();

                    
                    while (!gender.equalsIgnoreCase("Male") && !gender.equalsIgnoreCase("Female")) {
                        System.out.print("Input Candidate's Gender [Male | Female]: ");
                        gender = oop.nextLine();
                
                    if (!gender.equalsIgnoreCase("Male") && !gender.equalsIgnoreCase("Female")) {
                        System.out.println("Gender must be male or female!");
                    }
                }
                    
                    
                    boolean valid = false;
                    while (!valid) {
                    System.out.print("Input Candidate's Address [Must be ended with 'street']: ");
                    address = oop.nextLine();
                    if (address.endsWith("street")) {
                        valid = true;
                    } else {
                        System.out.print("");
                    }
                }


                    do {
                        System.out.print("Input Candidate's Age: ");
                        age = oop.nextInt();
                    } while (age < 17 || age > 30);

                    System.out.println("\nThank you for registering! Your initial is: "+initial);

                    Candidate candidate = new Candidate(name, gender, address, age, initial);
                    candidates[idx] = candidate;
                    idx++;
                    break;

                    
                case 2:
                    for (int i=0; i<idx-1;i++) {
                        for (int j=0;j<idx-i-1;j++) {
                            if (candidates[j].name.compareTo(candidates[j+1].name)>0) {
                                Candidate temp = candidates[j];
                                candidates[j] = candidates[j+1];
                                candidates[j+1] = temp;
                            }
                        }
                    }

                    if(idx == 0) {
                        System.out.println("\nNo Data!\n");
                    }
                    else {
                        System.out.println();
                        bubbleSort(candidates, idx);
                        for(int i=0; i<idx;i++) {
                            System.out.println(i+1 + " | " + candidates[i].name + " | " + candidates[i].initial + " | " + candidates[i].gender + " | "+ candidates[i].age + " | " + candidates[i].address + " | ");
                        }
                    }
                    break;

                case 3:
                    if(idx == 0) {
                        System.out.println("\nNo Data!\n");
                    }
                    else {
                        System.out.println();
                        bubbleSort(candidates, idx);
                        for(int i=0; i<idx;i++) {
                            System.out.println(i+1 + " | " + candidates[i].name + " | " + candidates[i].initial + " | " + candidates[i].gender + " | "+ candidates[i].age + " | " + candidates[i].address + " | ");
                        }
                    }
                    
                    if (idx>0) {
                    System.out.print("\nInput candidate to be removed [1..."+idx+"] [0 for cancel]: ");
                    int candidateNumber = oop.nextInt();

                    if (candidateNumber == 0) {
                        System.out.println("Deletion Canceled!");
                    } else if (candidateNumber >=1 && candidateNumber <=idx) {
                        removeCandidate (candidateNumber);

                    } else {
                        System.out.println("Invalid candidate number!");
                    }
                    }

                    break;

                    default:
                        inputOk = true;
                        System.out.println();
                    break;    
            }
        } while (choose != 4 || inputOk == false);

        oop.close();
    }

    static void bubbleSort(Candidate candidates[], int n) {
        int i, j;
        Candidate temp;
        for (i=0; i<n-1;i++) {
            for (j=0; j<n-i-1; j++) {
                if (candidates[j].name.compareTo(candidates[j+i].name)>0) {
                    temp = candidates[j];
                    candidates[j] = candidates[j+1];
                    candidates[j+1] = temp;
                }
            }
        }
    }
}
