# Jupyter notebook background실행
```python
import sys
old_stdout = sys.stdout
sys.stdout = open('./log.txt', 'w')

from IPython.lib import backgroundjobs as bg
jobs = bg.BackgroundJobManager()
def bgfunc():
  {Background 실행문}
jobs.new(bgfunc)

sys.stdout = old_stdout
jobs.status()
!tail -f log.txt
```
