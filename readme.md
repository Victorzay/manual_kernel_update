# Домашняя работа

 # Настройка окружения git

Так как я работаю в Windows 10, то возникли небольшие проблемы с некоторыми скриптами и конфигурационными файлами. При анализе проблемы выяснил,
 что связано это с разными стандартами концов строк в **_Windows_** и ___Unix___.
 
Поэтому сначала необходимо настроить git - 
 
 * $ git config --global core.autocrlf input
 * $ git config --global core.safecrlf warn
 
 Теперь файлы будут сохраняться в  формате ___Unix___ и проблем не будет.
 
 
 # Установка дополнений Virtualbox Guest Additions

Для автоматической установки дополнений ___Virtualbox Guest Additions___ установил плагин для ___Vagrant___ -

`vagrant plugin install vagrant-vbguest`

Также необходимы исходники ядра, установка для нашего обновленного ядра - 

`sudo yum install kernel-ml-devel`

При установке допополнений ___Virtualbox Guest Additions___ на новые ядра версии 5.4 и 5.12 из репозитория _epel-kernel_ тоже возникли проблемы, изучение которых привело меня к мысли,
 что требуется новая версия компилятора ___gcc___. После установки ___Developer Toolset 8___ по инструкции - <https://www.softwarecollections.org/en/scls/rhscl/devtoolset-8/> 
 дополнения скомпилировались и установились.
 
 Теперь можно включить ___synced_folders___ в ___Vagrantfile___, добавив в него -
 
 `config.vm.synced_folder "./shared", "/shared", type: "virtualbox"`
 
 Синхронизация общей папки работает.
 
 # Packer
 
 Немного отредактировал конфигурацию _centos.json_ для соответствия версии - 
 
```
    "artifact_description": "CentOS 7.9 with kernel 5.x",    
    "artifact_version": "7.9.2009",
    "image_name": "centos-7.9"
```
И при работе программы возникли проблемы с ___sudo___ при обработке скрипта, решил проблему сначала так - заменил команду создания файла /etc/sudoers.d/vagrant в файле vagrant.ks на такую команду:

`echo "vagrant ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/vagrant`

Но потом нашел инфу как настроить ___git___, см. п. **Настройка окружения git**

Ссылка на готовый образ  <https://app.vagrantup.com/Victorzay/boxes/centos-7-9>


