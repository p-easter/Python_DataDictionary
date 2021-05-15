# Python Data Dictionary Automation

## link to Medium Article.  

## Simple python class to rapidly develop a data dictionary for your data science projects.  

    class create_data_dictionary:
    
        def __init__(self):
            '''This class provides functions to quickly develop a data dictionary for your data set'''
            return None

        def make_my_data_dictionary(self, dataFrame):
            '''Create an initial data dictionary excluding definitions for meaning of features'''

            col_ = dataFrame.columns
            df_DataDict = {}

            for col in col_:
                    df_DataDict[col] = {
                                   'Type': str(df.dtypes[col]),
                                   'Length': len(df[col]),
                                   'Null_Count': sum(df[col].isna()),
                                   'Size(Memory)': df.memory_usage()[col],
                                   'Definition': str('')
                                    }

            df_DD = pd.DataFrame(df_DataDict)

            return df_DD

        def define_data_meaning(self, df_data_dictionary):
            '''Quickly provide input regarding each columns meaning and transpose into a usable dictionary'''

            col_ = df_data_dictionary.columns
            d = 'Definition'

            for col in col_:
                df_data_dictionary[col][d] = input('Provide a data definition for {}'.format(col))

            df_data_dictionary = df_data_dictionary.transpose()

            return df_data_dictionary

        def update_dd_definition(self, df_data_dictionary, attribute):
            try:
                df_dd = df_data_dictionary.transpose()
                df_dd[attribute]['Definition'] = input('Provide a data definition for {}'.format(attribute))
                df_dd = df_dd.transpose()
                return df_dd
            except:
                print('Sorry, there was an error.  Check attribute name and try again')

    Example use case:

    df = pd.read_csv('Some data you have')
    dd = create_data_dictionary()
    df_dd = dd.make_my_data_dictionary(df)
    df_dd = dd.define_data_meaning(df_dd)

    print(df_dd)

Output will be your data dictionary.  You can always go back and update your definitions by simply calling:

    df_dd = dd.update_dd_definition(df_dd, 'Name of one of your data dictionary attributes')
