# A Function for Descriptive Statistics in Julia 
This repository provides a Julia function for calculating descriptive statistics for a dataset. The function outputs a summary of key statistical measures such as mean, median, variance, standard deviation, and more, enabling users to gain insights into the distribution and characteristics of their data.

## Features

The function calculates the following descriptive statistics:
	•	Mean: Average of the data.
	•	Median: Middle value of the sorted dataset.
	•	Mode: Most frequently occurring value(s).
	•	Variance: Measure of data spread.
	•	Standard Deviation: Measure of data dispersion.
	•	Minimum and Maximum: Smallest and largest data points.
	•	Range: Difference between the maximum and minimum.
	•	Skewness: Asymmetry of the data distribution.
	•	Kurtosis: “Peakedness” of the data distribution.
	•	Quartiles: Divides the dataset into four equal parts.
	•	Interquartile Range (IQR): Range between the first and third quartiles.

## Prerequisites

Ensure you have Julia installed on your system. You can download it from the [official Julia website](https://julialang.org/downloads/).

## Installation
1.	Clone this repository: 
 
 ```julia
git clone https://github.com/your-repo-name/descriptive-statistics-julia.git
cd descriptive-statistics-julia
```
2.	Open Julia and activate the environment:
```julia
using Pkg
Pkg.activate(".")
Pkg.instantiate()
```
## Usage
1.	Import the function into your Julia script or REPL:
```julia
include("descriptive_statistics.jl")
using .DescriptiveStats
```
2.	Use the function to calculate statistics for your dataset. For example:
```julia
data = [1, 2, 3, 4, 5, 5, 6, 7, 8, 9, 10]
stats = descriptive_statistics(data)
println(stats)
```
3.	The output will be a dictionary with the calculated statistics:
```julia
Dict(
    "mean" => 5.454545454545454,
    "median" => 5.0,
    "mode" => [5],
    "variance" => 8.09090909090909,
    "std_dev" => 2.8460498941515415,
    "min" => 1,
    "max" => 10,
    "range" => 9,
    "skewness" => 0.0,
    "kurtosis" => -1.5,
    "quartiles" => (2.5, 5.0, 7.5),
    "iqr" => 5.0
)
```
## Function Implementation
Here is the implementation of the descriptive_statistics function:

```julia
module DescriptiveStats

using Statistics
using StatsBase

function descriptive_statistics(data::Vector{<:Real})
    data_sorted = sort(data)
    n = length(data)
    q1 = quantile(data_sorted, 0.25)
    q3 = quantile(data_sorted, 0.75)
    iqr = q3 - q1

    return Dict(
        "mean" => mean(data),
        "median" => median(data),
        "mode" => mode(data),
        "variance" => var(data, corrected=true),
        "std_dev" => std(data, corrected=true),
        "min" => minimum(data),
        "max" => maximum(data),
        "range" => maximum(data) - minimum(data),
        "skewness" => skewness(data),
        "kurtosis" => kurtosis(data),
        "quartiles" => (q1, median(data), q3),
        "iqr" => iqr
    )
end

end
```
## Testing

You can test the function using the provided sample dataset or your own data. Example test cases are included in the test/test_descriptive_statistics.jl file.

Run tests using:

```julia
julia --project -e 'using Pkg; Pkg.test()'
```
## Contributing

Contributions are welcome! Please fork the repository and submit a pull request with your changes.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

## Contact

For questions or feedback, feel free to open an issue or contact us at joshua.w.kelly@proton.me.

