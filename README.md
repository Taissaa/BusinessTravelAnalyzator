# BusinessTravelAnalyzator
Приложение для анализа данных по командировкам
```mermaid
---
tittle: BusinessTravelAnalyzator
---

classDiagram 
class FileReaderFactory{
    +create_fil_reader(file_path: str, file_format: str) -> FileReader
}
class FileReader{
    +String file_path
    +String file_format
    +read_data() -> List [Trip]
}
class JSONReader{
    +read_data()
}
class CSVReader{
    +read_data()
}
<<Abstract>> FileReader
class Employee {
    +String employee_id
    +String name
    +String department
    +trips: List[Trip]
    +add_trip(trip: Trip)
    +get_trip_statistics() -> Dictionary
}
class Trip {
    +String trip_id
    +String employee_id
    +String destination
    +Datetime date 
    +Float expenses
    +List [string] payment_methods
    +List [Expense] expenses
}
class Expense{
    +String expense_id
    +Float amount
    +String description
    +Datetime date
}
class ExpenseType{
    +String type_id
    +String type_name
}
class TravelExpense {
    +String transportation_method
}
class AccommodationExpense {
    +String hotel_name
    +Int nights
}
class MealExpense {
    +String restaurant_name
    +String meal_type
}
class ExpenseManager {
    +expense_types: List[ExpenseType]
    +get_expense_type(expense_id: str) -> ExpenseType
}
class AnalysisCreator {
    +createDataAnalythics()
}
<<Abstract>> AnalysisCreator
class SimpleAnalyzerCreator{
    +createDataAnalytics() -> Analyzer
}

class Analyzer{
    +employees: List[Employee]
    +trips: List[Trip]
    +most_frequent_destination() -> String
    +average_expenses() -> Float
    +employee_trip_frequency(employee_id: str) -> Int
    +yee_favorite_destination(employee_id: str) -> String
}

class ReportGenerator{
    +analyzer: Analyzer
    +generate_summary_report() -> String
    +generate_employee_report(employee_id: str) -> String
}
class DetailedReportDecorator{
    +__init__(self, report_generator: ReportGenerator)
    +generate_summary_report(self) -> String
}
class Visualizer{
    +analyzer: Analyzer
    +plot_trip_frequencies()
    +plot_expenses_distribution()
    +plot_top_destinations()
}
class ReportView
class GraphView
class TripController

FileReader <|-- JSONReader
FileReader <|-- CSVReader
FileReader --o FileReaderFactory
Trip *--  Employee
Analyzer --o Trip 
Analyzer --o Employee 
DetailedReportDecorator --o ReportGenerator
Visualizer --o Analyzer
ReportGenerator --o Analyzer
TripController --o ReportView
TripController --o GraphView
TripController ..> Analyzer
ReportView ..> ReportGenerator
GraphView ..> Analyzer
AnalysisCreator <|-- SimpleAnalyzerCreator
Analyzer --o AnalysisCreator
