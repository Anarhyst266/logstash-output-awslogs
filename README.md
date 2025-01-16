
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
