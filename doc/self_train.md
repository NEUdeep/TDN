## somthing
2021.0629

`just like below, one epoch cost 1.52h when we trained in 2*nvidia2080ti batch(8); 100 epoch cost 3day 6h.`

`python -m torch.distributed.launch --master_port 12347 --nproc_per_node=2 \
        main.py  something RGB --arch resnet50 --num_segments 8 --gd 20 --lr 0.02 \
        --lr_scheduler step  --lr_steps 50 75 90 --epochs 100 --batch-size 8 \
        --wd 1e-4 --dropout 0.5 --consensus_type=avg --eval-freq=1 -j 4 --npb --decoded_type decord`

- 8x1x1

something: 174 classes

​    Initializing TSN with base model: resnet50.

​    TSN Configurations:

​        input_modality:     RGB

​        num_segments:       8

​        new_length:         1

​        consensus_module:   avg

​        dropout_ratio:      0.8

​        img_feature_dim:    256   

=> base model: resnet50

video number:11522

video 0 done, total 0/11522, average 0.13565 sec/video, moving Prec@1 53.125 Prec@5 87.500

video 640 done, total 640/11522, average 0.01348 sec/video, moving Prec@1 53.869 Prec@5 81.994

video 1280 done, total 1280/11522, average 0.01007 sec/video, moving Prec@1 52.515 Prec@5 79.878

video 1920 done, total 1920/11522, average 0.00890 sec/video, moving Prec@1 50.717 Prec@5 79.764

video 2560 done, total 2560/11522, average 0.00826 sec/video, moving Prec@1 50.772 Prec@5 79.745

video 3200 done, total 3200/11522, average 0.00791 sec/video, moving Prec@1 50.712 Prec@5 80.043

video 3840 done, total 3840/11522, average 0.00779 sec/video, moving Prec@1 50.181 Prec@5 79.029

video 4480 done, total 4480/11522, average 0.00767 sec/video, moving Prec@1 49.734 Prec@5 78.723

video 5120 done, total 5120/11522, average 0.00761 sec/video, moving Prec@1 49.398 Prec@5 78.339

video 5760 done, total 5760/11522, average 0.00747 sec/video, moving Prec@1 49.793 Prec@5 78.349

video 6400 done, total 6400/11522, average 0.00738 sec/video, moving Prec@1 49.642 Prec@5 78.467

video 7040 done, total 7040/11522, average 0.00735 sec/video, moving Prec@1 49.675 Prec@5 78.606

video 7680 done, total 7680/11522, average 0.00728 sec/video, moving Prec@1 49.637 Prec@5 78.410

video 8320 done, total 8320/11522, average 0.00722 sec/video, moving Prec@1 49.521 Prec@5 78.388

video 8960 done, total 8960/11522, average 0.00720 sec/video, moving Prec@1 49.322 Prec@5 78.392

video 9600 done, total 9600/11522, average 0.00714 sec/video, moving Prec@1 49.346 Prec@5 78.457

video 10240 done, total 10240/11522, average 0.00709 sec/video, moving Prec@1 49.426 Prec@5 78.631

video 10880 done, total 10880/11522, average 0.00705 sec/video, moving Prec@1 49.578 Prec@5 78.620

video 11520 done, total 11520/11522, average 0.00702 sec/video, moving Prec@1 49.644 Prec@5 78.676

100%|████████████████████████████████████████████████████████| 11522/11522 [00:00<00:00, 63475.77it/s]

-----Evaluation is finished------

Overall Prec@1 49.64% Prec@5 78.68%

but origin is :top1=52.3%; maybe our parameters is not good; and found lr and wd is not good; the origin paper use `lr=0.01,wd=5e-4,--lr_steps  30 45 55 --epochs 60`, our lr is double of paper, maybe this is reason.