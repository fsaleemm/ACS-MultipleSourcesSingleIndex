# Azure Cognitive Search - Multiple Sources Indexed In Single Index

## Background
There are scenarios and use cases for creating an enerprise search experience where data from multiple sources can be searched in a single interface. This repo documents one of the patterns.
A pattern to merge data from multiple data sources into a single index is document in the [Index from multiple data sources using the .NET SDK](https://docs.microsoft.com/en-us/azure/search/tutorial-multiple-data-sources) tutorial.
This repo is based on the merging data pattern tutorial.

Our scenario is to index data from multiple sources into a single schema to enable unified search experience, where users search, sort, navigate, and view the data in the same manner.

## Architecture
The diagram below is a pattern used to create the unified search index. For simplicity, only 2 data sources are shown, however, the idea can be expanded as many [data sources supported](https://docs.microsoft.com/en-us/azure/search/search-indexer-overview#supported-data-sources) by Azure Cognitive Search.

![](/media/s1.png)

The key to this approach is the need for a “globalid”. Identify the combination of attributes that can be unique across all data sources. In the specific example above, the combination of source name and the record Id defines the “globalid”. E.g., <source name><unique Id> => Hotels12.

## Setup & Execute
1. Follow the tutorial [Index from multiple data sources using the .NET SDK](https://docs.microsoft.com/en-us/azure/search/tutorial-multiple-data-sources) to setup the Cosmos DB, Blob Storage.
1. Clone this git repository.
1. [Setup the environment](https://docs.microsoft.com/en-us/azure/search/tutorial-multiple-data-sources#2---set-up-your-environment) and appsettings.json with values from your environment.
1. Build the solution
```bash
cd ACS-MultipleSourcesSingleIndex
dotnet build
```
1. Run the project
```bash
dotnet run --project src/AzureSearchMultipleDataSources.csproj
```
![](/media/s6.png)

## Result
1. Sign in to the Azure Portal and navigate to your search service.
1. Under Indexes you will see as below
![](/media/s3.png)
1. Under Indexers you will see as below
![](/media/s4.png)
1. Under Data sources you will see as below
![](/media/s5.png)
1. Perform a "*" search in the Search explorer, you will get 2 results back, one from each source.
![](/media/s7.png)