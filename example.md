## Пример использования PlantUML на Python
```cmd
python -m pip install plantuml six
```

```python
from plantuml import PlantUML
from pathlib import Path

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

# Сохраняем описание в 
Path("use_case_diagram.puml").write_text(use_case_diagram)

# Конвертируем в PNG (требуется Java и plantuml.jar)
try:
    server = PlantUML(url="plantuml-1.2022.1.jar") 
    server.processes_file("use_case_diagram.puml", "use_case_diagram.png")
except Exception as e:
    print(f"Произошла ошибка при конвертации диаграммы: {e}")
else:
    print("Диаграмма сохранена в use_case_diagram.png")
```
