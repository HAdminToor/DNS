# DNS

### Модуль 2: Организация сетевого администрирования
## **Задание модуля 2**

**1. Настройте DNS-сервер на сервере HQ-SRV:**  
**a. На DNS сервере необходимо настроить 2 зоны**

**Зона hq.work**  
| Имя | Тип записи | Адрес |
| :---         |     :---:      |          ---: |
| hq-r.hq.work   | A, PTR     | IP-адрес    |
| hq-srv.hq.work   | A, PTR     | IP-адрес    |  

**Зона branch.work**  
| Имя | Тип записи | Адрес |
| :---         |     :---:      |          ---: |
| br-r.branch.work   | A, PTR     | IP-адрес    |
| br-srv.branch.work   | A     | IP-адрес    |  

## **HQ-SRV**  

```
nano /etc/bind/options.conf
```
![image](https://github.com/NyashMan/DEMO2024/assets/1348639/d903e095-bbe6-4050-b473-a475d2fd5d46)  

```
systemctl enable --now bind
nano /etc/bind/local.conf
```
![image](https://github.com/NyashMan/DEMO2024/assets/1348639/754ad3e6-64da-4fa4-ad12-22e05b21a960)  
```
cp /etc/bind/zone/{localdomain,hq.db}
cp /etc/bind/zone/{localdomain,branch.db}
cp /etc/bind/zone/{127.in-addr.arpa,0.db}
cp /etc/bind/zone/{127.in-addr.arpa,2.db}
chown root:named /etc/bind/zone/{hq,branch,0,2}.db
nano /etc/bind/zone/hq.db
```
Обратите внимание на синтаксис. Проверьте точки в конце наименований зон!
![image](https://github.com/NyashMan/DEMO2024/assets/1348639/e81f251c-9987-4d8d-ad47-e4ae50d99e1d)  
```
nano /etc/bind/zone/branch.db
```
![image](https://github.com/NyashMan/DEMO2024/assets/1348639/b2740789-a372-40f4-8558-b12afeb85d78)  
```
nano /etc/bind/zone/0.db
```
![image](https://github.com/NyashMan/DEMO2024/assets/1348639/b4239e96-7018-4286-8861-ea53aa074e85)  
```
nano /etc/bind/zone/2.db
```
![image](https://github.com/NyashMan/DEMO2024/assets/1348639/9cc74901-aa52-49be-a2b7-6afa65803b3c)  
```
systemctl restart bind
```
Выполняем проверку:  

![image](https://github.com/NyashMan/DEMO2024/assets/1348639/030310e9-e147-4465-8266-f16a628c6152)  

Если настройка была выполнена верно, то вы увидети прямые и обратные зоны DNS.  
