---
title: c++决策树代码分析
abbrlink: ea3d45b1
date: 2023-11-17 16:49:43
tags:
categories: 学习笔记
cover: https://images.pexels.com/photos/11879973/pexels-photo-11879973.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1
---



# 代码

```c++
 * @Description: C++实现决策树
 * @Author: szq
 * @Github: https://github.com/MrQqqq
 * @Date: 2020-06-29 01:31:54
 * @LastEditors: szq
 * @LastEditTime: 2020-07-08 18:57:10
 * @FilePath: \cpp\src\DecisionTree\DecisionTree.cpp
 */

#include<iostream>
#include<math.h>
#include<algorithm>
#include"DecisionTree.h"
using namespace std;

/**
 * @destription: 导入数据
 * @param {type} trainData：训练数据  trainLabel：训练标签
 * @return: 没有返回值
 */
void DecisionTree::loadData(vector<vector<int>>& trainData, vector<int>& trainLabel) {
    //如果数据特征向量的数量和数据集标签的数量不一样的时候，数据有问题
    if (trainData.size() != trainLabel.size()) {
        cerr << "input error" << endl;
        return;
    }
    //初始化
    this->trainData = trainData;
    this->trainLabel = trainLabel;

    //计算featureValues
    for (auto data : trainData) {
        for (int i = 0; i < data.size(); ++i) {
            featureValues[i].insert(data[i]);
        }
    }
}

/**
 * @destription: 统计数据集中每个标签的数量，比如结果为1的数量和结果为2的数量
 * @param {type} dataset：数据集，是训练数据的子集，整型数组表示，每一个整数表示第几个训练数据
 * @return: 标签名，标签数的map
 */
map<int, int> DecisionTree::labelCount(vector<int>& dataset) {
    map<int, int> res;
    //遍历数据集，统计标签出现的次数
    for (int index : dataset) {
        res[trainLabel[index]]++;
    }
    return res;
}

/**
 * @destription: 计算信息熵，公式为-pi * log(pi)求和
 * @param {type} ：dataset：数据集
 * @return: 信息熵
 */

double DecisionTree::caculateEntropy(vector<int>& dataset) {
    map<int, int> label_count = labelCount(dataset);
    int len = dataset.size();
    double result = 0;
    for (auto count : label_count) {
        double pi = count.second / static_cast<double>(len);
        result -= pi * log2(pi);
    }
    return result;
}

/**
 * @destription: 根据特征名来划分子集
 * @param {type} dataset：数据集
 * @param feature:第几个特征
 * @param value:第几个特征的特征值
 * @return: 返回划分的子集
 */
vector<int> DecisionTree::splitDataset(vector<int>& dataset, int& feature, int& value) {
    vector<int> res;
    for (int index : dataset) {
        if (trainData[index][feature] == value) {
            res.push_back(index);
        }
    }
    return res;
}

/**
 * @destription: 计算信息熵
 * @param {type}
 * @return:
 */
double DecisionTree::caculateGain(vector<int>& dataset, int& feature) {
    set<int> values = featureValues[feature];
    double result = 0;
    for (int value : values) {
        vector<int> subDataset = splitDataset(dataset, feature, value);
        result += subDataset.size() / static_cast<double>(dataset.size()) * caculateEntropy(subDataset);
    }
    return caculateEntropy(dataset) - result;

}

/**
 * @destription: 获取标签统计中出现次数最多的标签
 * @param labelCount:标签统计
 * @return: 返回出现次数最多的标签名
 */
int DecisionTree::getMaxTimesLabel(map<int, int>& labelCount) {
    int max_count = 0;
    int res;
    for (auto label : labelCount) {
        if (max_count <= label.second) {
            max_count = label.second;
            res = label.first;
        }
    }
    return res;
}

/**
 * @destription: 获取特征集信息增益中最大的信息增益和所对应的特征
 * @param gains:特征集的信息增益
 * @return: 最大信息增益对应的特征
 */
int DecisionTree::getMaxGainFeature(map<int, double>& gains) {
    double max_gain = 0;
    int max_gain_feature;
    for (auto gain : gains) {
        if (max_gain <= gain.second) {
            max_gain = gain.second;
            max_gain_feature = gain.first;
        }
    }
    return max_gain_feature;
}

/**
 * @destription: 创建决策树
 * @param dataset:数据集
 * @param features:特征集
 * @return: 返回决策树根节点指针
 */
TreeNode* DecisionTree::createTree(vector<int>& dataset, vector<int>& features) {
    TreeNode* root = new TreeNode();
    map<int, int> label_count = labelCount(dataset);
    //如果特征集为空，则该树为单节点树，类别为标签中出现次数最多的标签
    if (features.size() == 0) {
        root->result = getMaxTimesLabel(label_count);
        root->isLeaf = true;
        return root;
    }
    //如果数据集中只包含一种标签，则该树为单节点树，类别为该标签
    if (label_count.size() == 1) {
        root->result = label_count.begin()->first;
        root->isLeaf = true;
        return root;
    }

    //计算特征集中每个特征的信息增益
    map<int, double> gains;
    for (int feature : features) {
        gains[feature] = caculateGain(dataset, feature);
    }

    //获取最大信息增益的特征和最大的信息增益
    int max_gain_feature = getMaxGainFeature(gains);
    vector<int> subFeatures = features;
    subFeatures.erase(find(subFeatures.begin(), subFeatures.end(), max_gain_feature));
    for (int value : featureValues[max_gain_feature]) {
        TreeNode* branch = new TreeNode();//创建分支
        vector<int> subDataset = splitDataset(dataset, max_gain_feature, value);


        //如果子集为空，将分支节点标记为叶节点，类别为标签中出现次数最多的标签
        if (subDataset.size() == 0) {
            branch->isLeaf = true;
            branch->result = getMaxTimesLabel(label_count);
            branch->attr = max_gain_feature;
            branch->attr_value = value;
            root->branchs.push_back(branch);
        }
        //否则递归创建树
        else {
            branch = createTree(subDataset, subFeatures);
            branch->attr = max_gain_feature;
            branch->attr_value = value;
            root->branchs.push_back(branch);
        }
    }
    return root;
}

/**
 * @destription: 构造函数
 * @param trainData:训练数据
 * @param trainLabel:训练数据标签
 * @param threshold:阈值
 * @return: 没有返回值
 */
DecisionTree::DecisionTree(vector<vector<int>>& trainData, vector<int>& trainLabel, int& threshold) {
    loadData(trainData, trainLabel);//导入数据
    this->threshold = threshold;//设置阈值
    vector<int> dataset(trainData.size());//数据集
    for (int i = 0; i < trainData.size(); i++) {
        dataset[i] = i;
    }
    vector<int> features(trainData[0].size());//属性集合
    for (int i = 0; i < trainData[0].size(); i++) {
        features[i] = i;
    }
    decisionTreeRoot = createTree(dataset, features);//创建决策树
}

/**
 * @destription: 分类
 * @param testData:测试数据
 * @param root:决策树根节点
 * @return: 返回分类结果
 */
int DecisionTree::classify(vector<int>& testData, TreeNode* root) {
    //如果决策树节点是叶子节点，直接返回结果
    if (root->isLeaf) {
        return root->result;
    }
    for (auto node : root->branchs) {
        //找到分支，并在分支中再细分
        if (testData[node->attr] == node->attr_value) {
            return classify(testData, node);
        }
    }
    return 0;
}


int main() {
    //训练数据
    vector<vector<int>> trainData = {
        {0, 0, 0, 0},
        {0, 0, 0, 1},
        {0, 1, 0, 1},
        {0, 1, 1, 0},
        {0, 0, 0, 0},
        {1, 0, 0, 0},
        {1, 0, 0, 1},
        {1, 1, 1, 1},
        {1, 0, 1, 2},
        {1, 0, 1, 2},
        {2, 0, 1, 2},
        {2, 0, 1, 1},
        {2, 1, 0, 1},
        {2, 1, 0, 2},
        {2, 0, 0, 0}
    };
    //训练标签
    vector<int> trainLabel = { 0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0 };
    int threshold = 0;
    DecisionTree dt = DecisionTree(trainData, trainLabel, threshold);

    //测试数据
    vector<int> testData = { 2,1,1,1 };
    TreeNode* root = dt.decisionTreeRoot;
    int type = dt.classify(testData, root);
    cout << type << endl;
    return 0;
}```
```



# 伪代码

导入所需的库

输入: 

训练数据 {0, 0, 0, 0},{0, 0, 0, 1}, {0, 1, 0, 1},{0, 1, 1, 0},……{2, 1, 0, 2},{2, 0, 0, 0} 

训练标签 trainLabel = {0, 0, 1, 1, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0};

 

过程：

1）创建计算的函数方法：

  1、创建 loadData 方法；检测数据是否正确并返回数据    

  2、创建 labelCount 方法：统计标签出现的次数

  3、创建 calculateEntropy 方法：计算信息熵，公式为-pi * log(pi)求和   

  4、创建 splitDataset 方法；根据特征名来划分子集 

  5、创建 calculateGain 方法：计算具体的信息增益 

  6、创建 getMaxTimesLabel 方法：得到出现次数最多的标签 

  7、创建 getMaxGainFeature 方法：获取特征集信息增益中最大的信息增益和所对应的特征

2） 创建 createTree决策树

​    1、接受数据集和特征集作为参数

​    2、创建根节点 root

​    3、获取标签统计 label_count

​    4、if 特征集为空，将根节点设为叶子节点，类别为标签中出现次数最多的标签，  

递归返回，情形 (1)

​    5、if数据集中只包含一种标签，将根节点设为叶子节点，类别为该标签，

递归返回，情形 (2)

 

选择最优划分属性向：

​    6、计算特征集中每个特征的信息增益，存储在 gains 中（calculateEntropy 方法）

​    7、获取最大信息增益的特征和最大的信息增益（calculateGain 方法）

8、继续生成子树：

​    	1\创建一个分支节点 branch

​    	2\遍历最大信息增益特征的每个可能取值 value

​      3\创建一个子数据集 subDataset 通过调用 splitDataset 方法

​      4\如果子数据集为空，将分支节点标记为叶节点，类别为标签中出现次数最多的标签	

   递归返回，情形 (3)

​      5\否则，递归调用 createTree 方法创建子树，并将子树添加到分支节点

​      6\将分支节点添加到根节点的分支列表中

​    	7\返回根节点

​    

3）创建 DecisionTree 构造函数

​    1、接受训练数据、训练数据标签和阈值作为参数

​    2、调用 loadData 方法导入数据

​    3、设置阈值 threshold

​    4、创建数据集 dataset，初始化为包含所有数据点的索引

​    5、创建特征集 features，初始化为包含所有特征的索引

​    6、调用 createTree 方法创建决策树，并将根节点存储在 decisionTreeRoot 中

​    

 4）创建 classify 方法：（目的是为了分类）

​    1、接受测试数据和根节点作为参数

​    2、如果根节点是叶子节点，直接返回结果

​    3、遍历根节点的每个分支

​      找到匹配测试数据的分支，然后递归调用 classify 方法

​    4、return返回分类结果

​    

5）主函数 main 中

  1、定义训练数据 trainData 和训练标签 trainLabel

  2、创建 DecisionTree 对象 dt，传入 trainData、trainLabel 和阈值 threshold

  3、定义测试数据 testData：调用 classify 方法对测试数据进行分类，传入决策树的根节点，将结果存储在 type 变量中

  4、输出分类结果

 

输出: 以 node 为根结点的决策树

 
