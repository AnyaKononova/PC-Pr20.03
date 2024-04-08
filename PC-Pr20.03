#include <iostream>
#include <string>
#include <opencv2/core.hpp>
#include <opencv2/imgproc.hpp>
#include <opencv2/highgui.hpp>

void image2grayScale(cv::Mat& input, cv::Mat& output);
void image2Sepia(cv::Mat& input, cv::Mat& output);
void image2Negative(cv::Mat& input, cv::Mat& output);
void findContour(cv::Mat& input, cv::Mat& output);

int main(void) {
    std::string image_path = cv::samples::findFile("C:/Users/Nuta/Documents/Open MP/Практика 20.03/pic2.jpg");
    cv::Mat image = cv::imread(image_path, cv::IMREAD_COLOR);
    cv::Mat grayScale, sepia, negative, contour;

    if (image.empty()) {
        std::cout << "Could not read the image: " << image_path << std::endl;
        return 1;
    }

    image2grayScale(image, grayScale);
    image2Sepia(image, sepia);
    image2Negative(image, negative);
    findContour(image, contour);

    cv::imshow("original", image);
    cv::imshow("gray", grayScale);
    cv::imshow("sepia", sepia);
    cv::imshow("negative", negative);
    cv::imshow("contour", contour);

    cv::imwrite("original.jpg", image);
    cv::imwrite("gray.jpg", grayScale);
    cv::imwrite("sepia.jpg", sepia);
    cv::imwrite("negative.jpg", negative);
    cv::imwrite("contour.jpg", contour);

    cv::waitKey(0);
    return 0;
}

void findContour(cv::Mat& input, cv::Mat& output) {
    cv::Mat grayScale;
    cv::cvtColor(input, grayScale, cv::COLOR_BGR2GRAY);

    cv::Mat contour_img = cv::Mat::zeros(input.size(), CV_8UC1);

    for (int i = 1; i < grayScale.rows - 1; ++i) {
        for (int j = 1; j < grayScale.cols - 1; ++j) {
            float gx = grayScale.at<uchar>(i + 1, j + 1) + 2 * grayScale.at<uchar>(i, j + 1) + grayScale.at<uchar>(i - 1, j + 1) - grayScale.at<uchar>(i + 1, j - 1) - 2 * grayScale.at<uchar>(i, j - 1) - grayScale.at<uchar>(i - 1, j - 1);
            float gy = grayScale.at<uchar>(i + 1, j + 1) + 2 * grayScale.at<uchar>(i + 1, j) + grayScale.at<uchar>(i + 1, j - 1) - grayScale.at<uchar>(i - 1, j - 1) - 2 * grayScale.at<uchar>(i - 1, j) - grayScale.at<uchar>(i - 1, j + 1);
            contour_img.at<uchar>(i, j) = 255 - sqrt(pow(gx, 2) + pow(gy, 2));
        }
    }
    contour_img.copyTo(output);
}

void image2grayScale(cv::Mat& input, cv::Mat& output) {
    cv::cvtColor(input, output, cv::COLOR_BGR2GRAY);
}

void image2Sepia(cv::Mat& input, cv::Mat& output) {
    cv::Mat sepiaScale = cv::Mat::zeros(input.size(), CV_8UC3);
    cv::cvtColor(input, sepiaScale, cv::COLOR_BGR2RGB);
    output = sepiaScale;
}

void image2Negative(cv::Mat& input, cv::Mat& output) {
    cv::Mat negative_img = cv::Mat::zeros(input.size(), CV_8UC3);
    cv::bitwise_not(input, negative_img);
    output = negative_img;
}
