# laba7
Laba 7 Mobilki (TepluhinLev 803a2)

1) Создаём новый проект
2) Добавялем поле PlaneText, TextView, 2 кнопки "Save" "Load"

![image](https://user-images.githubusercontent.com/78772701/140328668-059bf374-3db6-49fa-86c8-f6a99843a3d2.png)

3) Назначим имя файла и установим путь для него
```Java
public class MainActivity extends AppCompatActivity {

    String filename = "content.txt";
    File file;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        file = new File(MainActivity.this.getFilesDir(),filename);
    }
```
4) Напишем обработчик события для кнопки "Save"
```Java
public void saveClick(View view) {
        try
        {
            EditText textBox = (EditText) findViewById(R.id.editTextTextPersonName);
            String text = textBox.getText().toString();
            FileOutputStream fos = new FileOutputStream(file);
            fos.write(text.getBytes());
            fos.close();
            Toast.makeText(this, "Текстовый файл успешно сохранён!",
                    Toast.LENGTH_SHORT).show();
        }
        catch (FileNotFoundException e)
        {
            e.printStackTrace();
            Toast.makeText(this, "Файл не найден!",
                    Toast.LENGTH_SHORT).show();
        }
        catch (IOException e)
        {
            e.printStackTrace();
            Toast.makeText(this, "Ошибка сохранения файла!",
                    Toast.LENGTH_SHORT).show();
        }
    }
```
5) Напишем обработчик события для кнопки "Load"
```Java
public void openClick(View view) {
        try
        {
            FileInputStream fin = new FileInputStream(file);
            byte[] bytes = new byte[fin.available()];
            fin.read(bytes);
            String text = new String(bytes);
            TextView textView = (TextView) findViewById(R.id.textView);
            textView.setText(text);
            fin.close();
        }
        catch (IOException ex)
        {
            Toast.makeText(this, ex.getMessage(),
                    Toast.LENGTH_SHORT).show();
        }
    }
```
6) Установим разрешение на доступ в файле "AndroidManifest.xml"
```Java
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.savereadfile">

    <uses-permission
        android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission
        android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```
7) Запускаем и проверяем

![S11104-210006](https://user-images.githubusercontent.com/78772701/140329645-8b142ccc-7e6a-414f-87b3-0d63c3b2eed0.jpg)
![S11104-210021](https://user-images.githubusercontent.com/78772701/140329941-de24d3f4-a6f1-4c4f-b70f-73c9da38d171.jpg)
![S11104-210025](https://user-images.githubusercontent.com/78772701/140329970-f1921c52-483a-429a-86ea-da619196efc3.jpg)
