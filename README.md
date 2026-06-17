<build> 
                              <plugins> 
                              <plugin> 
                              <artifactId>maven-jar-plugin</artifactId> 
                              <version>3.1.0</version> 
                              <configuration> 
                                     <archive> 
                                     <manifest> 
                                             <addClasspath>true</addClasspath> 
                                             <mainClass>com.multit.App</mainClass>  <!-- Replace with main class  
                                    </manifest> 
                                   </archive> 
                             </configuration> 
                           </plugin> 
                         </plugins> 
                         </build> 
deploy ---
- name: Deploy JAR
  hosts: local
  become: false

  tasks:
    - name: Copy JAR file
      copy:
        src: /mnt/c/ProgramData/Jenkins/.jenkins/workspace/Maven-CI/target/flipkart-app-1.0-SNAPSHOT.jar
        dest: /home/meghana/ansible-lab/app.jar
        mode: '0755'

    - name: Run JAR file
      shell: nohup java -jar /home/meghana/ansible-lab/app.jar > app.log 2>&1 &

7 ---
- name: Install htop system monitor tool
  hosts: local
  become: false

  tasks:
    - name: Install htop package
      ansible.builtin.package:
        name: htop
        state: present
