# laba7
Laba 7 Mobilki (TepluhinLev 803a2)

1) Создаём новый проект
2) Добавялем поле PlaneText, 
   TextView, 2 кнопки "Save" "Load"

![image](https://user-images.githubusercontent.com/73265867/143829847-acd9b0b7-5cc3-4830-b02d-aee18224a382.png)

3) Назначил имя файла и установил путь 
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
4) Обработчик события для кнопки Save
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
5) Обработчик события для кнопки "Load
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
6) Установим разрешение на доступ
```Java
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.savereadfile">

    <uses-permission
        android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission
        android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```
7) Проверяем и запускаем приложение

Начальный экран
![image](https://user-images.githubusercontent.com/73265867/143829927-16712cb2-849f-427c-bd9f-3b4d338300ac.png)
Пишем в поле PlaneText слово "privet" и нажимаем кнопку Save: выдает сообщение "Текстовый файл успешно сохранен".
![image](https://user-images.githubusercontent.com/73265867/143830996-3fef607f-a2e9-432b-a81d-c65d652fb8ec.png)
Нажимае кнопку Load в поле TextView отображаеться "privet".
![image](https://user-images.githubusercontent.com/73265867/143831176-6c3fe8d3-57c5-4196-a73c-6a8c7dfc607a.png)


