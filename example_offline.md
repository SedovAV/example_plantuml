## Пример использования PlantUML на Python (offline версия)
```cmd
python -m pip install plantuml six
```

```python
from pathlib import Path
import subprocess

use_case_diagram = """
@startuml
left to right direction
actor Покупатель as Customer
actor Администратор as Admin

rectangle "Онлайн-магазин" {
  usecase "Просмотр товаров" as UC1
  usecase "Оформление заказа" as UC2
  usecase "Управление товарами" as UC3
  usecase "Анализ продаж" as UC4

  Customer --> UC1
  Customer --> UC2
  Admin --> UC3
  Admin --> UC4
}

Customer --> UC3 : Расширенные права
@enduml
"""

# Сохраняем описание в файл
Path("use_case_diagram.puml").write_text(use_case_diagram)

# Запускаем PlantUML через командную строку
jar_path = r"plantuml-1.2022.1.jar"
try:
    result = subprocess.run(
        ["java", "-jar", jar_path, "use_case_diagram.puml"],
        check=True,
        capture_output=True,
        text=True
    )
    print("Диаграмма успешно сгенерирована в use_case_diagram.png")
except subprocess.CalledProcessError as e:
    print(f"Ошибка при запуске PlantUML: {e.stderr}")
except FileNotFoundError:
    print("Ошибка: Проверьте, установлен ли Java и правильный ли путь к plantuml.jar")
except Exception as e:
    print(f"Произошла ошибка: {e}")```
### Результат:
<img src="/use_case_diagram.png" width="600"/>
