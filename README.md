name: weixin
on:
  workflow_dispatch:
  schedule: 
    # 代表国际标准时间4点0分，北京时间需要+8小时，代表北京时间中午12点运行
    - cron: '0 8 * * *'
jobs:
#将工作流程中运行的所有作业组合在一起
  build:
  #定义名为 build 的作业。 子键将定义作业的属性 
    runs-on: ubuntu-latest 
    steps:
      - uses: actions/checkout@v2
    
      - name: Set up Python 3.9
        uses: actions/setup-python@v2
        with:
          python-version: 3.9.1
      - name: install pip packages
        run: |
          python -m pip install --upgrade pip
          pip3 install -r requirements.txt
      - name: weixin
        run: |
          python3 main.py
