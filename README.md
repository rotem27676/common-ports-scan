import socket
from colorama import Fore, Style, init

# colorama
init(autoreset=True)

def check_port(host, port):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(1)  # one sec max per test
    result = sock.connect_ex((host, port))
    sock.close()
    return result == 0

# common ports
common_ports = [21, 22, 23, 25, 53, 80, 110, 143, 443, 445, 587, 993, 995, 3306, 8080]

host = "localhost"  # target ip

# port scan
for port in common_ports:
    is_open = check_port(host, port)
    status_color = Fore.GREEN if is_open else Fore.RED
    status_text = "open" if is_open else "closed"
    print(f"Port {Fore.YELLOW}{port}{Style.RESET_ALL} is {status_color}{status_text}{Style.RESET_ALL}")
