# bot-phonebook #

Contoh ini akan mendemonstrasikan cara untuk membuat sebuah aplikasi bot dengan **Spring framework** dan terintegrasi dengan **LINE Messaging API** dan **Line Bot SDK**, **PostgreSQL** untuk registrasi dan mendapatkan data dari bot yang layaknya sebuah buku telepon yang dikirimkan oleh pengguna via LINE Chat ke aplikasi bot anda. Aplikasi ini dijalankan di **Heroku**.

### Langkah Untuk Membuat ###
* Pertama, anda harus membuat akun LINE@, mengaktifkan Messaging API, menambahkan *add-on* PostgreSQL pada Heoku anda, dan memasukkan URL dari Webhook anda.

* Selanjutnya, tambah file  `application.properties` di direktori *src/main/resources*, dan isi dengan channel secret dan channel access token anda, seperti berikut:

	```ini
com.linecorp.channel_secret=<your_channel_secret>
com.linecorp.channel_access_token=<your_channel_access_token>
	```
	
* Lalu, siapkan tabel untuk menyimpan data yang akan digunakan oleh aplikasi ini. Untuk mengakses PostgreSQL dari heroku adalah sebagai berikut:

	```bash
	$ heroku psql
	```
	Siapkan tabel yang akan digunakan.

	```sql
	CREATE TABLE IF NOT EXISTS phonebook
	(
		id BIGSERIAL PRIMARY KEY,
		name TEXT,
		phone_number TEXT
	);
	```	
* Kemudian, siapkan DAO di sisi client. DAO berfungsi untuk memanipulasi data yang terdapat dalam database.

	```java
	public interface PersonDao
{
    	public List<Person> get();
    	public List<Person> getByName(String aName);
    	public int registerPerson(String aName, String aPhoneNumber);
};

	```
	
* Untuk mengimplementasikan DAO, dibutuhkan query-query untuk melakukan manipulasi data yang ada didalam database. Manipulasi data yang dilakukan pada contoh ini menggunakan potongan-potongan kode di bawah ini.
	
	Potongan kode ini digunakan untuk registrasi buku telepon baru ke database
	
	```java
    private final static String SQL_REGISTER="INSERT INTO phonebook (name, phone_number) VALUES (?, ?);";
    
    public int registerPerson(String aName, String aPhoneNumber)
    {
        return mJdbc.update(SQL_REGISTER, new Object[]{aName, aPhoneNumber});
    }
	```
	
	Potongan kode ini digunakan untuk mengambil seluruh data
	
	```java
	private final static String SQL_SELECT_ALL="SELECT id, name, phone_number FROM phonebook";
    
    private final static ResultSetExtractor< List<Person> > MULTIPLE_RS_EXTRACTOR=new ResultSetExtractor< List<Person> >()
    {
        @Override
        public List<Person> extractData(ResultSet aRs)
            throws SQLException, DataAccessException
        {
            List<Person> list=new Vector<Person>();
            while(aRs.next())
            {
                Person p=new Person(
                aRs.getLong("id"),
                aRs.getString("name"),
                aRs.getString("phone_number"));
                list.add(p);
            }
            return list;
        }
    };
    
    public List<Person> get()
    {
        return mJdbc.query(SQL_SELECT_ALL, MULTIPLE_RS_EXTRACTOR);
    }
	```
	Potongan kode ini digunakan untuk mengambil data dengan nama tertentu
	
	```java
	private final static String SQL_SELECT_ALL="SELECT id, name, phone_number FROM phonebook";
    private final static String SQL_GET_BY_NAME=SQL_SELECT_ALL + " WHERE LOWER(name) LIKE LOWER(?);";
    
    private final static ResultSetExtractor<Person> SINGLE_RS_EXTRACTOR=new ResultSetExtractor<Person>()
    {
        @Override
        public Person extractData(ResultSet aRs)
				throws SQLException, DataAccessException
        {
            while(aRs.next())
            {
                Person p=new Person(
                    aRs.getLong("id"),
                    aRs.getString("name"),
                    aRs.getString("phone_number"));
                return p;
            }
            return null;
        }
    };
    
    public List<Person> getByName(String aName)
    {
        return mJdbc.query(SQL_GET_BY_NAME, new Object[]{"%"+aName+"%"}, MULTIPLE_RS_EXTRACTOR);
    }
	```

*  Untuk mengakses fungsi pada DAO, dilakukan dengan cara berikut:

	```java
	List<Person> self=mDao.getByName("%"+aName+"%");
	```
* Setelah selesai membuat aplikasi anda, anda dapat menjalankan aplikasi anda.
* Penggunaan
    
    Ada dua kata kunci yang bisa digunakan dengan bot ini, yaitu **find** dan **reg**

Template pesan untuk find:
> find "Your_Name"<br><br>
> **INFO** Tanda kutip dua (") harus digunakan. Jika tidak digunakan, maka katakunci tidak akan dikenali oleh bot.
    
Template pesan untuk reg:
> reg "Your_Name" #Your_Phone_Number<br><br>
> **INFO** Tanda kutip dua (") dan tanda pagar (#) harus digunakan. Jika tidak digunakan, maka kata kunci tidak akan dikenali oleh bot.


### Tautan ke git repository ###

[bot-phonebook](https://github.com/line-indonesia/bot-phonebook)
