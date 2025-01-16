**# Logstash Plugin

This is a plugin for [Logstash](https://github.com/elastic/logstash).

It is fully free and fully open source. The license is Apache 2.0, meaning you are pretty much free to use it however you want in whatever way.

## Documentation

Logstash provides infrastructure to automatically generate documentation for this plugin. We use the asciidoc format to write documentation so any comments in the source code will be first converted into asciidoc and then into html. All plugin documentation are placed under one [central location](http://www.elastic.co/guide/en/logstash/current/).

- For formatting code or config example, you can use the asciidoc `[source,ruby]` directive
- For more asciidoc formatting tips, see the excellent reference here https://github.com/elastic/docs#asciidoc-guide

## Need Help?

Need help? Try #logstash on freenode IRC or the https://discuss.elastic.co/c/logstash discussion forum.

## Developing

### 1. Plugin Developement and Testing

#### Code
- To get started, you'll need JRuby with the Bundler gem installed.

- Create a new plugin or clone and existing from the GitHub [logstash-plugins](https://github.com/logstash-plugins) organization. We also provide [example plugins](https://github.com/logstash-plugins?query=example).

- Install dependencies
```sh
bundle install
```

#### Test

- Update your dependencies

```sh
bundle install
```

- Run tests

```sh
bundle exec rspec
```

### 2. Running your unpublished Plugin in Logstash

#### 2.1 Run in a local Logstash clone

- Edit Logstash `Gemfile` and add the local plugin path, for example:
```ruby
gem "logstash-filter-awesome", :path => "/your/local/logstash-filter-awesome"
```
- Install plugin
```sh
bin/logstash-plugin install --no-verify
```
- Run Logstash with your plugin
```sh
bin/logstash -e 'filter {awesome {}}'
```
At this point any modifications to the plugin code will be applied to this local Logstash setup. After modifying the plugin, simply rerun Logstash.

#### 2.2 Run in an installed Logstash

You can use the same **2.1** method to run your plugin in an installed Logstash by editing its `Gemfile` and pointing the `:path` to your local plugin development directory or you can build the gem and install it using:

- Build your plugin gem
```sh
gem build logstash-filter-awesome.gemspec
```
- Install the plugin from the Logstash home
```sh
bin/logstash-plugin install /your/local/plugin/logstash-filter-awesome.gem
```
- Start Logstash and proceed to test the plugin

## Contributing

All contributions are welcome: ideas, patches, documentation, bug reports, complaints, and even something you drew up on a napkin.

Programming is not a required skill. Whatever you've seen about open source and maintainers or community members  saying "send patches or die" - you will not see that here.

It is more important to the community that you are able to contribute.

For more information about contributing, see the [CONTRIBUTING](https://github.com/elastic/logstash/blob/master/CONTRIBUTING.md) file.
**
# Logstash Output Plugin for AWS CloudWatch Logs

This plugin for [Logstash](https://www.elastic.co/logstash) allows you to send events to [AWS CloudWatch Logs](https://aws.amazon.com/cloudwatch/).

## Installation

The plugin is published on [RubyGems](https://rubygems.org/). You can install it directly using the `logstash-plugin` command:

```bash
logstash-plugin install logstash-output-awslogs
```

Ensure that you have Logstash installed and properly configured before proceeding.

## Usage

After installing the plugin, add it to your Logstash configuration file:

```logstash
output {
  awslogs {
    access_key_id => "YOUR_ACCESS_KEY_ID"
    secret_access_key => "YOUR_SECRET_ACCESS_KEY"
    region => "us-east-1"
    log_group_name => "your_log_group_name"
    log_stream_name => "your_log_stream_name"
  }
}
```

### Alternative Configuration Options

1. **Using AWS Session Token**:
   If your environment requires temporary credentials with a session token, you can include it as follows:

   ```logstash
   output {
     awslogs {
       access_key_id => "YOUR_ACCESS_KEY_ID"
       secret_access_key => "YOUR_SECRET_ACCESS_KEY"
       session_token => "YOUR_SESSION_TOKEN"
       region => "us-east-1"
       log_group_name => "your_log_group_name"
       log_stream_name => "your_log_stream_name"
     }
   }
   ```

2. **Using IRSA (IAM Roles for Service Accounts)**:
   If you are running Logstash in an environment like Amazon EKS or EC2, where IAM roles are available, you can omit `access_key_id`, `secret_access_key`, and `session_token`. The plugin will automatically use the IAM role assigned to the service account or instance.

   ```logstash
   output {
     awslogs {
       region => "us-east-1"
       log_group_name => "your_log_group_name"
       log_stream_name => "your_log_stream_name"
     }
   }
   ```

   Ensure that the IAM role has the necessary permissions to write to CloudWatch Logs.

### Parameters:

- `access_key_id`: Your AWS Access Key ID.
- `secret_access_key`: Your AWS Secret Access Key.
- `session_token`: (Optional) Your AWS session token for temporary credentials.
- `region`: AWS Region (e.g., `us-east-1`).
- `log_group_name`: The name of the CloudWatch Logs group.
- `log_stream_name`: The name of the CloudWatch Logs stream.

Make sure the provided AWS credentials or IAM roles have sufficient permissions to write to CloudWatch Logs.

## Development

1. Clone the repository:

   ```bash
   git clone https://github.com/Anarhyst266/logstash-output-awslogs.git
   ```

2. Navigate to the plugin directory:

   ```bash
   cd logstash-output-awslogs
   ```

3. Install dependencies:

   ```bash
   bundle install
   ```

4. For local testing with Logstash:
   - Clone the Logstash repository.
   - In the `Gemfile` of Logstash, add the following line:

     ```ruby
     gem "logstash-output-awslogs", :path => "/path/to/your/plugin"
     ```

   - Install the plugin:

     ```bash
     bin/logstash-plugin install --no-verify
     ```

   - Start Logstash with your configuration.

## Contribution

Contributions are welcome! Please create [issues](https://github.com/Anarhyst266/logstash-output-awslogs/issues) or submit pull requests to help improve the project.

## License

This project is licensed under the Apache 2.0 License. See the [LICENSE](https://github.com/Anarhyst266/logstash-output-awslogs/blob/master/LICENSE) file for details.

## Acknowledgments

This plugin is based on the work by [RickyCook](https://github.com/RickyCook/logstash-output-awslogs).
