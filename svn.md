# SVN - Subversion
SVN digunakan untuk versioning coding. Sehingga setiap perubahan akan kelihatan History nya yaitu seperti Siapa yang mengedit, delete, add. Atau Jika ada kerusakan atau kesalahan cukup back to version sebelumnya.

## Installasi & Setting SVN
* Install SVN  
	`apt-get install subversion subversion-tools`

* Buat folder SVN  
	`mkdir /svn`

* Passang hak akses menggunakan service libapache2  
	`chown -R www-data: /svn`

* Configure Apache  
	`sudo a2enmod dav_svn`

* Edit apache2 configurasi  
	`cd /etc/apache2`  
	`nano apache2.conf`  
	ubah setting :
		
		<Location /svn>
		 DAV svn
		 SVNParentPath /home/svn
		 AuthType Basic
		 AuthName "My SVN Repositories"
		 AuthUserFile /etc/svn-auth
		 Require valid-user
		</Location>

* Masuk ke SVN Folder dan buat Folder baru untuk menampung versioning data.  
	`cd /svn`  
	`svnadmin create MFTL`

* Tambahkan hak akses ke folder MFTL Tersebut  
	`chown -R www-data:www-data MFTL`

* Untuk Add User bisa dengan Perintah  
	`htpasswd -cm /etc/svn-auth nunung`

* Untuk Edit password User dengan perintah  
	`htpasswd  /etc/svn-auth arif`

## Create New Project
Untuk membuat project, masuk ke browser dan buka jenkins
1. Klik New Item
2. Ketik nama project dan Pilih Freestyle Project, lalu klik OK
3. Centang Subversion dan masukkan URL SVN dari project.
4. Pilih credentials, Kalo belum ada buat dulu.
5. Repository Dept Pilih infinity
6. Lalu Save

Tahap diatas adalah tahap menjalankan SVN Update. Untuk menjalankan sonarqube untuk inspeksi quality control maka 
1. Klik Nama Project
2. Klik Configure
3. Pada Add Build Step, pilih execute shell.
4. Input perintah untuk menjalankan Sonar.
