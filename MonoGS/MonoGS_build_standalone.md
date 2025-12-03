# MonoGS_build.md

## MonoGS

### 环境

```bash
git clone https://github.com/muskie82/MonoGS.git --recursive
cd MonoGS
```

可将 "torchaudio"注释掉：

```shell
mamba env create -f environment.yml -y
mamba activate MonoGS
```



### issues

#### CUDA Out of Memory

utils/slam_frontend，line 164，`torch.cuda.empty_cache()`

```shell
for tracking_itr in range(self.tracking_itr_num):
    torch.cuda.empty_cache() # Add this line to clear CUDA cache and free memory
    render_pkg = render(
        viewpoint, self.gaussians, self.pipeline_params, self.background
    )
    image, depth, opacity = (
        render_pkg["render"],
        render_pkg["depth"],
        render_pkg["opacity"],
    )
    pose_optimizer.zero_grad()
    loss_tracking = get_loss_tracking(
        self.config, image, depth, opacity, viewpoint
    )
```



#### 服务器无gui

```bash
echo 'export LIBGL_ALWAYS_SOFTWARE=1' >> ~/.bashrc
source ~/.bashrc
```



#### ？

```shell
/home/ha/Desktop/rec/MonoGS/utils/eval_utils.py:50: RuntimeWarning: More than 20 figures have been opened. Figures created through the pyplot interface (`matplotlib.pyplot.figure`) are retained until explicitly closed and may consume too much memory. (To control this warning, see the rcParam `figure.max_open_warning`).
  fig = plt.figure()
```



```shell
[W CudaIPCTypes.cpp:15] Producer process has been terminated before all shared CUDA tensors released. See Note [Sharing CUDA tensors]
```



```shell
distCUDA2(torch.from_numpy(np.asarray(pcd.points)).float().cuda()),
RuntimeError: tabulate: failed to synchronize: cudaErrorInvalidConfiguration: invalid configuration argument
```

the initialised depth map is too sparse and the module failed to calculate nearest neighbor
