<component name="RemoteRepositoriesConfiguration">
    <remote-repository>
      <option name="id" value="central" />
      <option name="name" value="Central Repository" />
      <option name="url" value="https://repo.maven.apache.org/maven2" />
    </remote-repository>
    <remote-repository>
      <option name="id" value="central" />
      <option name="name" value="Maven Central repository" />
      <option name="url" value="https://repo1.maven.org/maven2" />
    </remote-repository>

  
    <remote-repository>
      <option name="id" value="jboss.community" />
      <option name="name" value="JBoss Community repository" />
      <option name="url" value="https://repository.jboss.org/nexus/content/repositories/public/" />
    </remote-repository>
    <component name="ExternalStorageConfigurationManager" enabled="true" />
  <component name="MavenProjectsManager">
    <option name="originalFiles">
      <list>
        <option value="$PROJECT_DIR$/pom.xml" />
      </list>
    </option>
  </component>
  <component name="ProjectRootManager" version="2" languageLevel="JDK_22" default="true" project-jdk-name="openjdk-22" project-jdk-type="JavaSDK">
    <output url="file://$PROJECT_DIR$/out" />
  </component>


  <component name="AutoImportSettings">
    <option name="autoReloadType" value="SELECTIVE" />
  </component>
  <component name="ChangeListManager">
    <list default="true" id="a8a6cf17-11d9-478e-be36-e19ee5cd06c0" name="Changes" comment="" />
    <option name="SHOW_DIALOG" value="false" />
    <option name="HIGHLIGHT_CONFLICTS" value="true" />
    <option name="HIGHLIGHT_NON_ACTIVE_CHANGELIST" value="false" />
    <option name="LAST_RESOLUTION" value="IGNORE" />
  </component>
  <component name="ProjectColorInfo"><![CDATA[{
  "associatedIndex": 3
}]]></component>
  <component name="ProjectId" id="2kXIfLDprPJf0FwQvU6h8QwU3yc" />
  <component name="ProjectViewState">
    <option name="hideEmptyMiddlePackages" value="true" />
    <option name="showLibraryContents" value="true" />
  </component>
  <component name="PropertiesComponent"><![CDATA[{
  "keyToString": {
    "Application.GameLauncher.executor": "Run",
    "RunOnceActivity.ShowReadmeOnStart": "true",
    "kotlin-language-version-configured": "true",
    "onboarding.tips.debug.path": "C:/Users/aashi/IdeaProjects/New/src/main/java/org/example/Main.java"
  }
}]]></component>
  <component name="SpellCheckerSettings" RuntimeDictionaries="0" Folders="0" CustomDictionaries="0" DefaultDictionary="application-level" UseSingleDictionary="true" transferred="true" />
  <component name="TaskManager">
    <task active="true" id="Default" summary="Default task">
      <changelist id="a8a6cf17-11d9-478e-be36-e19ee5cd06c0" name="Changes" comment="" />
      <created>1723423599385</created>
      <option name="number" value="Default" />
      <option name="presentableId" value="Default" />
      <updated>1723423599385</updated>
    </task>
    

    main:
    import java.util.ArrayList;
import java.util.Scanner;
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class GeneticMonsters {
    public static void main(String[] args) {
        MonsterManager manager = new MonsterManager();
        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("1. Create Monster");
            System.out.println("2. View Monsters");
            System.out.println("3. Breed Monsters");
            System.out.println("4. Save Game");
            System.out.println("5. Load Game");
            System.out.println("6. Exit");
            System.out.println("7. return to menu");
            int choice = scanner.nextInt();
            switch (choice) {
                case 1:
                    createMonster(manager, scanner);
                    break;
                case 2:
                    viewMonsters(manager);
                    break;
                case 3:
                    breedMonsters(manager, scanner);
                    break;
                case 4:
                    saveGame(manager);
                    break;
                case 5:
                    loadGame(manager);
                    break;
                case 6:
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid");
                case 7:
                    System.return(0);
                    break;
                default:
                    System.out.print("Invalied");
            }
        }
    }

    public static void createMonster(MonsterManager manager, Scanner scanner) {
        System.out.print("Enter monster name: ");
        String name = scanner.next();

        System.out.print("Enter monster color: ");
        String color = scanner.next();

        int strength;
        do {
            System.out.print("Enter monster strength (1-100): ");
            strength = scanner.nextInt();
            if (strength < 1 || strength > 100) {
                System.out.println("Strength must be between 1 and 100. Please try again.");
            }
        } while (strength < 1 || strength > 100);

        int speed;
        do {
            System.out.print("Enter monster speed (1-100): ");
            speed = scanner.nextInt();
            if (speed < 1 || speed > 100) {
                System.out.println("Speed must be between 1 and 100. Please try again.");
            }
        } while (speed < 1 || speed > 100);

        Monster monster = new Monster(name, color, strength, speed);
        manager.addMonster(monster);
        System.out.println("Monster created successfully: " + monster);
    }

    public static void viewMonsters(MonsterManager manager) {
        manager.displayMonsters(true);
    }

    public static void breedMonsters(MonsterManager manager, Scanner scanner) {
        System.out.print("Enter index of first monster: ");
        int index1 = scanner.nextInt();
        System.out.print("Enter index of second monster: ");
        int index2 = scanner.nextInt();
        manager.breedMonsters(index1, index2);
    }

    public static void saveGame(MonsterManager manager) {
        FileManager.saveMonsters(manager.getMonsters(), "monsters_data.txt");
    }

    public static void loadGame(MonsterManager manager) {
        ArrayList<Monster> monsters = FileManager.loadMonsters("monsters_data.txt");
        manager.setMonsters(monsters);
        System.out.println("Game loaded successfully!");
    }
}

class Monster {
    private String name;
    private String color;
    private int strength;
    private int speed;

    public Monster(String name, String color, int strength, int speed) {
        this.name = name;
        this.color = color;
        this.strength = strength;
        this.speed = speed;
    }

    public String getName() {
        return name;
    }

    public String getColor() {
        return color;
    }

    public int getStrength() {
        return strength;
    }

    public int getSpeed() {
        return speed;
    }

    public void performSpecialAbility() {
        System.out.println("Performing special ability!");
    }

    public String toString() {
        return "Name: " + name + ", Color: " + color + ", Strength: " + strength + ", Speed: " + speed;
    }
}

class MonsterManager {
    private ArrayList<Monster> monsters;

    public MonsterManager() {
        monsters = new ArrayList<>();
    }

    public void addMonster(Monster m) {
        monsters.add(m);
    }

    public void breedMonsters(int index1, int index2) {
        if (index1 < 0 || index2 < 0 || index1 >= monsters.size() || index2 >= monsters.size()) {
            System.out.println("Invalid monster index");
            return;
        }

        Monster m1 = monsters.get(index1);
        Monster m2 = monsters.get(index2);

        // Breeding logic: Combining attributes of the two monsters
        String name = m1.getName().substring(0, m1.getName().length()/2) +
                      m2.getName().substring(m2.getName().length()/2);

        String color = m1.getColor() + "-" + m2.getColor();

        int strength = (m1.getStrength() + m2.getStrength()) / 2;
        int speed = (m1.getSpeed() + m2.getSpeed()) / 2;

        Monster offspring = new Monster(name, color, strength, speed);
        monsters.add(offspring);

        System.out.println("New monster created: " + offspring);
    }

    public void displayMonsters(boolean detailed) {
        for (Monster m : monsters) {
            if (detailed) {
                System.out.println(m.toString());
            } else {
                System.out.println(m.getName());
            }
        }
    }

    public ArrayList<Monster> getMonsters() {
        return monsters;
    }

    public void setMonsters(ArrayList<Monster> monsters) {
        this.monsters = monsters;
    }
}

class FileManager {
    public static void saveMonsters(ArrayList<Monster> monsters, String filename) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filename))) {
            for (Monster m : monsters) {
                writer.write(m.toString());
                writer.newLine();
            }
            System.out.println("Game saved successfully!");
        } catch (IOException e) {
            System.out.println("Error saving monsters: " + e.getMessage());
        }
    }

    public static ArrayList<Monster> loadMonsters(String filename) {
        ArrayList<Monster> monsters = new ArrayList<>();
        try (BufferedReader reader = new BufferedReader(new FileReader(filename))) {
            String line;
            while ((line = reader.readLine()) != null) {
                String[] parts = line.split(", ");
                String name = parts[0].split(": ")[1];
                String color = parts[1].split(": ")[1];
                int strength = Integer.parseInt(parts[2].split(": ")[1]);
                int speed = Integer.parseInt(parts[3].split(": ")[1]);
                monsters.add(new Monster(name, color, strength, speed));
            }
        } catch (IOException e) {
            System.out.println("Error loading monsters: " + e.getMessage());
        }
        return monsters;
    }
}
