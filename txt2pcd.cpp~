#include <boost/program_options.hpp>
#include <pcl/point_types.h>
#include <pcl/io/pcd_io.h>
#include <pcl/common/point_operators.h>
#include <pcl/common/io.h>
#include <pcl/search/organized.h>
#include <pcl/search/octree.h>
#include <pcl/search/kdtree.h>
#include <pcl/features/normal_3d_omp.h>
#include <pcl/filters/conditional_removal.h>
#include <pcl/segmentation/sac_segmentation.h>
#include <pcl/segmentation/extract_clusters.h>
#include <pcl/surface/gp3.h>
#include <pcl/io/vtk_io.h>
#include <pcl/filters/voxel_grid.h>
 
#include <iostream>
#include <fstream>
 
using namespace pcl;
using namespace std;
 
namespace po = boost::program_options;

// 定义点的类型
typedef struct TxtPoint
{
    double x;
    double y;
    double z;
    double I;
}POINT;
 
int main(int argc, char **argv){
	///The file to read from.
	string infile;
 
	///The file to output to.
	string outfile;
 
	// Declare the supported options.
	po::options_description desc("Program options");
	desc.add_options()
		//Options
		("infile", po::value<string>(&infile)->required(), "the file to read a point cloud from")
		("outfile", po::value<string>(&outfile)->required(), "the file to write the DoN point cloud & normals to")
		;
	// Parse the command line
	po::variables_map vm;
	po::store(po::parse_command_line(argc, argv, desc), vm);
 
	// Print help
	if (vm.count("help"))
	{
		cout << desc << "\n";
		return false;
	}

	// Process options.
	po::notify(vm);

//开始转
    int num_point;
    FILE *fp_txt;
    TxtPoint txtpoint;
    vector<TxtPoint> pcdpoints;
    pcl::PointCloud<pcl::PointXYZ>::Ptr cloud(new pcl::PointCloud<pcl::PointXYZ>);

    fp_txt=fopen(infile.c_str(), "r");
    if (fp_txt)
    {
        while (fscanf(fp_txt, "%lf %lf %lf", &txtpoint.x, &txtpoint.y, &txtpoint.z) !=EOF)
        {
            pcdpoints.push_back(txtpoint);
        }
    }
    else
        cout<<"fail to load .txt file"<<endl;
    
    num_point=pcdpoints.size();
    cloud->width=num_point;
    cloud->height=1;
    cloud->is_dense=false;
    cloud->points.resize(cloud->width * cloud->height);
    for (int i =0; i < cloud->points.size(); i++)
    {
        cloud->points[i].x=pcdpoints[i].x;
        cloud->points[i].y=pcdpoints[i].y;
        cloud->points[i].z=pcdpoints[i].z;

    }
    //output .pcd
    pcl::PCDWriter writer;
    writer.write(outfile, *cloud);
    //or use savePCDFile like the following code
    //pcl::io::savePCDFileASCII("outputfile.pcd", *cloud);
    cout<<"finished"<<endl;
   
    return 0;
 

}


