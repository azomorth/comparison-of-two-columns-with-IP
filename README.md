#check_ip_addresses
import pandas as pd

def check_ip_addresses(file_path, output_file='missing_ips.txt'):
    """
    Проверяет наличие IP-адресов из первого столбца в втором столбце файла Excel.
    Записывает отсутствующие IP-адреса в отдельный файл.

    Args:
        file_path (str): Путь к файлу Excel.
        output_file (str, optional): Путь к файлу с отсутствующими IP-адресами. Defaults to 'missing_ips.txt'.
    """

    df = pd.read_excel(file_path)
    ip_list_1 = df.iloc[:, 0].tolist()  # Получаем список IP-адресов из первого столбца
    ip_list_2 = df.iloc[:, 1].tolist()  # Получаем список IP-адресов из второго столбца

    missing_ips = []
    for ip in ip_list_1:
        if ip not in ip_list_2:
            missing_ips.append(ip)

    # Записываем отсутствующие IP-адреса в файл
    with open(output_file, 'w') as f:
        for ip in missing_ips:
            f.write(str(ip) + '\n')  # Преобразуем IP в строку перед записью

    print(f"Отсутствующие IP-адреса записаны в файл: {output_file}")

# Пример использования
file_path = 'D:\\1.xlsx'  # Замените на путь к вашему файлу

check_ip_addresses(file_path)
