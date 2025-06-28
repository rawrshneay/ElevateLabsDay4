# ElevateLabsDay4
Task 4 : Setup and Use a Firewall on Windows/Linux

First i make sure i have installed ufw on linux.

![image](https://github.com/user-attachments/assets/fe6e2caf-1ebb-4769-9dc8-545df6431eb1)

After that, i list the current firewall rules.

![image](https://github.com/user-attachments/assets/de94188f-ddfc-4cab-89ce-06e3dd7e87db)

sudo ufw enable
Activates the UFW firewall.
Ensures it starts automatically at system boot.
Output confirms the firewall is now active.

![image](https://github.com/user-attachments/assets/6d1e08d3-2b99-4e2c-b557-db48ee440921)


sudo ufw status numbered
Displays the current firewall rules with rule numbers.
Output shows: Status: active (but no rules yet).

![image](https://github.com/user-attachments/assets/bab1ade0-9fe9-4929-a595-d14dcdccc2ea)


sudo ufw deny 23
Adds a rule to block inbound traffic on port 23, used by Telnet.
Two rules are added:
One for IPv4: Rule added
One for IPv6: Rule added (v6)

![image](https://github.com/user-attachments/assets/54cf1703-5954-47eb-94f2-4c6052102794)


telnet localhost 23
Tries to connect to Telnet service on the local machine (port 23).

![image](https://github.com/user-attachments/assets/288ae723-f50d-4d9c-937d-036f4efb4206)

Result:
Connection refused from both ::1 (IPv6) and 127.0.0.1 (IPv4).
This means:
Either no Telnet server is running, or
The firewall rule is successfully blocking the connection.

sudo ufw status numbered
Lists all active firewall rules with their rule numbers.
Output shows:
[1] 23 DENY IN Anywhere
[2] 23 (v6) DENY IN Anywhere (v6)
This means port 23 is blocked for both IPv4 and IPv6.
Im listing it out to delete the rule based on the index number.

![image](https://github.com/user-attachments/assets/fc360917-5122-418e-a8a0-e2d1316399db)

sudo ufw delete 1
Deletes rule number 1, which blocks port 23 for IPv4.

![image](https://github.com/user-attachments/assets/a0af5f28-0af9-41ac-ac54-5a884166ab5d)

Prompt: Proceed with operation (y|n)?
You entered y → Rule deleted successfully.

sudo ufw status numbered 
Rechecks current firewall rules.

![image](https://github.com/user-attachments/assets/d8b8dcae-d25f-45d6-982f-b0ecc61bf47e)

Output now shows only:
[1] 23 (v6) DENY IN Anywhere (v6)
IPv4 rule is successfully removed, but IPv6 rule still exists.

How a Firewall Filters Work:
A firewall monitors and controls incoming and outgoing network traffic based on predefined security rules.
It acts as a barrier between a trusted internal network and untrusted external networks like the internet.
Firewalls use rules to decide whether to allow or block specific traffic.
How Filtering Works
Allow rules: Permit traffic on specific ports or from specific IP addresses.
Deny rules: Block traffic on certain ports or from specified IP addresses.
Inbound filtering: Controls traffic coming into the system.
Outbound filtering: Controls traffic leaving the system (less commonly used in UFW by default).
Rules are processed in the order they are listed; the first match is applied.
