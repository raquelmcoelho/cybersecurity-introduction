# Introduction - Cybersecurity

# **TP1 - Traffic Sniffing with Wireshark**

## **Objectives**

- Learn how to configure a virtual network.
- Learn how to filter data in Wireshark.
- Discover vulnerabilities in Telnet and HTTP services.

---

## **1. Virtualization Environment Setup**

1. Download and install the latest version of **VirtualBox**.
2. Download and install **Oracle VM VirtualBox Extension Pack**.

---

## **2. Virtual Machine Preparation**

1. Download the two virtual machines **"Student.ova"** and **"MyServer.ova"** from [this platform](https://foad.ensicaen.fr/).
2. Import these virtual machines into VirtualBox.
3. Discuss with your instructor how to set up the virtual network.
    
    ### File > Tools > Network Manager:
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image.png)
    
    ### {VM name} >  Settings > Network:
    
    Do these configurations on both of the machines. This allow us to to use the network we created which includes the host, making it possible the sniffing by the host.
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%201.png)
    
    ### Host’s terminal:
    
    ```bash
    	sudo ip link set vboxnet0 promisc on # before starting VMs
    ```
    
4. Start the **"Student" VM** and log in with the credentials: **student | student**.
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%202.png)
    
5. Start the **"MyServer" VM** and log in with: **student | ensicaen**.
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%203.png)
    
6. Assign an **IP address** to each virtual machine.
    
    ### Server’s terminal:
    
    ```bash
    sudo nano /etc/network/interfaces # add new ip based on our network
    ```
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%204.png)
    
    ### Student’s terminal:
    
    ```bash
    sudo ip addr flush dev enp0s3 # clean up old ip
    sudo ip addr add 192.168.56.2/24 dev enp0s3 # adding new ip/netmask based on our network
    ```
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%205.png)
    
7. Verify connectivity between the two VMs.
    - The **MyServer VM** should **not** have access to the internet.
    
    ### Doing ping from server to student ✅
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%206.png)
    

---

## **3. Capturing Telnet Passwords**

1. On the **Student** machine, open a terminal and run the command:
    
    ```bash
    whoami
    ```
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%207.png)
    
2. Open **Wireshark** and select the correct network interface for traffic capture.
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%208.png)
    
3. Start packet capture in Wireshark.
    
    ### Testing packet capture with our network ✅
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%209.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2010.png)
    
4. Open a terminal and run:
    
    ```bash
    telnet <MyServer IP>
    ```
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2011.png)
    
5. Log in using the **MyServer** credentials.
6. Run `whoami` again and explain the output.
    
    After connecting to the **MyServer** machine via **Telnet** and running the `whoami` command, the terminal will display the authenticated user on MyServer.
    
    - **If the login is successful**, the output will be:
        
        ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2012.png)
        
        This confirms that authentication was successful and that the user "student" has access to the remote system.
        
7. Stop the traffic capture in Wireshark.
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2013.png)
    
8. Analyze the captured traffic and apply filters to isolate **Telnet** data.
9. Identify and extract the **username and password** exchanged during the session.
    
    ### Login ✅
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2014.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/00d157bc-d1f6-4538-a156-02f3534fc7f4.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2015.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2016.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2017.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2018.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2019.png)
    
    ### Password ✅
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2020.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2021.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2022.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2023.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2024.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2025.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2026.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2027.png)
    
10. Type **"quit"** to exit the Telnet session.
11. What solution can be implemented to **secure authentication data**?
    
    The **Telnet** protocol does not provide encryption, making it highly vulnerable to sniffing attacks. 
    
    **Replace Telnet with SSH:**
    
    - **SSH (Secure Shell)** encrypts communications, preventing credential capture.
    - SSH supports **public key authentication**, eliminating the need to send passwords over the network.

---

## **4. Capturing HTTP Data**

1. Start a **new capture** in Wireshark.
2. Open **Firefox** browser.
3. In the address bar, enter:
    
    ```
    http://<MyServer IP>
    ```
    
4. Click on the **"DVWA"** link.
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2028.png)
    
5. On the login page, enter the credentials:
    
    ```
    admin | password
    ```
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2029.png)
    
6. Once logged in, stop the packet capture.
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2030.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2031.png)
    
7. Analyze the captured traffic and apply filters for **HTTP traffic**.
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2032.png)
    
    ![image.png](Introduction%20-%20Cybersecurity%2019e9f2956718800c95dcce1214d55e48/image%2033.png)
    
8. What solution can be implemented to **secure authentication data**?
    
    The **HTTP** protocol also transmits data in **plaintext**, meaning credentials can be easily intercepted. Solutions to protect authentication data include:
    
    **1 - Use HTTPS (HyperText Transfer Protocol Secure)**
    
    - HTTPS uses **TLS/SSL** to encrypt data between the client and the server.
    
    **2 - Implement token-based authentication**
    
    - Methods like **OAuth, JWT (JSON Web Token)**, or **encrypted session cookies** prevent credentials from being repeatedly sent.
    
    **3 - Enable HSTS (HTTP Strict Transport Security)**
    
    - HSTS forces browsers to always use HTTPS when communicating with the server.

---

## **Troubleshooting Errors**

If you encounter errors such as:

```
E: Could not get lock /var/lib/dpkg/lock-frontend - open (11: Resource temporarily unavailable)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?

```

Try running the following commands:

```bash
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock*
sudo dpkg --configure -a
sudo apt update

```