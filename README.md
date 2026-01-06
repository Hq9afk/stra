# Smart Task Resource Allocator (STRA)

A system based on a machine learning model (Decision Tree) to predict the required resource level (low / medium / high) for each AI task, helping to allocate resources efficiently in an operating system or cloud environment.

---

## Environment Requirements

- Python 3.8+
- Libraries:
  ```bash
  pip install -r requirements.txt
  ```

---

## How to Run

### Step 1: Collect task metrics

```bash
python generate_input_data.py
```
- Task metrics are collected and classified based on resource-consumption
- Collected data are used as input for AI model
- Saves data to `data/input_data.csv`
### Step 2: Train the Model

```bash
python model/train_model.py
```

- Reads data from `data/train_data.csv`
- Saves the model to `model/model.pkl`

---

### Step 3: Single Prediction (CLI)

```bash
python main.py
```

- Enter task information:
  ```
  Task type: data_analysis
  CPU usage (%): 50
  Memory usage (%): 40
  I/O usage (%): 30
  Duration (s): 60
  Priority: medium
  ```
- Result:
  ```
  Predicted resource allocation: MEDIUM
  ```

---

### Step 4: Batch Prediction from CSV

```bash
python -c "from model import predictor; predictor.predict_from_csv('data/input_data.csv', 'data/output_data.csv')"
```

- Prints results to terminal
- Writes to `data/output.csv` 

---

### Step 5: Quick Test

```bash
python test/test_prediction.py
```

- Runs a sample example to check the system
- Prints result to screen

---

## Sample Data (`train_data.csv`)

```csv
task_type,cpu_usage,mem_usage,io_usage,duration,priority,resource_allocated
System Idle Process,2094,0,0,0,unknown,medium
System,16,0,100,8126,low,medium
unknown,0,0,0,8127,low,medium
Registry,0,0,100,8128,low,medium
smss.exe,0,0,0,8126,low,medium
svchost.exe,0,0,0,8123,low,medium
...
```

---

## Notes

- Tasks are automatically encoded using an internal mapping table.
- Can be extended to other models such as Random Forest, Logistic Regression.
- Suitable for OS environments, container schedulers, or cloud resource planners.
