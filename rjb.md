# CUDA and Pytorch Installation for QD-GGA

If error is:

```
ImportError: /lib/x86_64-linux-gnu/libstdc++.so.6: version `GLIBCXX_3.4.29' not found (required by /home/as1211/miniconda3/envs/qdgga_new/lib/python3.8/site-packages/google/protobuf/pyext/_message.cpython-38-x86_64-linux-gnu.so)
ERROR:torch.distributed.elastic.multiprocessing.api:failed (exitcode: 1) local_rank: 0 (pid: 278249) of binary: /home/as1211/miniconda3/envs/qdgga_new/bin/python
```

Then, update libstdc++6

```bash
sudo add-apt-repository ppa:ubuntu-toolchain-r/test # Ignore if not ubuntu
sudo apt-get update
sudo apt-get install gcc-4.9
sudo apt-get upgrade libstdc++6
sudo apt-get dist-upgrade
```

Also, make sure to confirm the necessary dependencies are installed for the right GLIBCXX version.
```bash
strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBCXX
```

Not required but if does not work, try this too:

```bash
conda install libgcc
conda install -c conda-forge ncurses
```

Install requirements and torch properly
```bash
pip install -r requirements_new.txt
pip install torch==1.13.1+cu117 torchvision==0.14.1+cu117 torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/cu117
```
