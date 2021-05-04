# niitopng
# This is python code which will code your .nii formate images into png




# import these libraries if you have install otherwise install it
import os
import nibabel as nib
import imageio








def nii_to_image(filepath):
    # Read nii folder
    filenames = os.listdir(filepath)
    
    # Start reading nii file
    for f in filenames:
        img_path = os.path.join(filepath, f)
        img = nib.load(img_path)  # Read nii
        img_fdata = img.get_fdata()
        # Remove the suffix of nii
        fname = f.replace('.nii', '')  
        img_f_path = os.path.join(imgfile, fname)

        # Create a folder of images corresponding to nii
        if not os.path.exists(img_f_path):
            # new folder
            os.mkdir(img_f_path)  

        # Start converting to image
        (x, y, z) = img.shape
        # z is the sequence of images
        for i in range(z):
            # Choose which direction to slice
            silce = img_fdata[:, :, i]
            # Save image
            imageio.imwrite(os.path.join(img_f_path, '{}.png'.format(i)), silce)
            
            
            
if __name__ == '__main__':
    filepath = 'E:/Master/MICCAI_BraTS2020_TrainingData/BraTS20_Training_003/'
    nii_to_image(filepath)
