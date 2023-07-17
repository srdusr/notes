
Planning to develop some python application or python package your best option is use virtual environments.
Try virtualenv or even conda

Use poetry much better option to manage application from start to finish. It is a much better option than requirements.txt + setup.py.


Another more simple option is use python-virtualenv. This can bring portability to the code and maintain old packages as well. Install it with

sudo pacman -S python-virtualenv

and then do this

virtualenv -p /usr/bin/python3 yourenv
source yourenv/bin/activate
pip install package-name

When you create this environment yourenv, you will setup pip to install packages only into this environment, not to the entire system.
