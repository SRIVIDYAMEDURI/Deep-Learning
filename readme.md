## 8. Jupyter Notebooks

The same code can also be run via notebooks. From AMLWorkbench, click File --> Open Command-Line Interface to launch the CLI shell in the project folder, then enter the following command:

* first you need to install Jupyter Python package

```
C:\Temp\Iris> pip install notebook
```

* launch Jupyter server from the local project folder

```
C:\Temp\Iris> az ml notebook
```

This will start the notebook server and display a URL you can use to connect from any web browser on your machine (by default this is http://localhost:8888). Additionally, it also launches Jupyter web UI from this address using your default browser automatically as shown below. Create a new notebook as shown below.

![Jupyter]()
![Rename]()

You will also notice a notebook file (.pynb) created in Notebooks tab of AMLWorkbench as shown below. Run the code from CATelcoCustomerChurnModeling.py via notebook. Alternatively, you can also open ChurnAnalytics.ipynb that contains markdown comments to run the code in the notebook.

![ChurnAnalytics]()



